# Healthcare Data Mapping Assistant

**Shelia Howard · DSC670 Advanced Uses of Generative AI · Bellevue University**

I built a Streamlit prototype to help healthcare data analysts review how incoming demographic fields map to a shared schema. The prototype accepts a source field name, datatype, description, and optional synthetic example value. It proposes one of 13 approved destinations or returns `REVIEW`, with a rationale and a human-review flag. An analyst can accept, revise, reject, or hold a recommendation.

[View the presentation and application screenshots](evidence/milestone-4-presentation.pdf)

## Problem and scope

A source field such as `patientDOB` can map directly to `date_of_birth`. A field containing a person's full name is different because the target schema stores given and family names separately. The analyst needs to determine how to split the field before it can be mapped. The project focuses on this distinction within patient and member demographics, including identifiers, names, dates of birth, administrative sex, addresses, and contact information.

## Data and methods

1. **Prompt design.** I authored a 30-row synthetic metadata dataset and compared six GPT-4o mini prompts on the same six cases. These included three direct mappings and three ambiguous cases. Adding an explicit review option raised target accuracy from 3/6 with the controlled-schema prompt to 5/6 with the explicit review prompt. The six-case exercise informed the schema and response contract.
2. **Fine-tuning.** I used Hugging Face Transformers to fully fine-tune Qwen2.5-0.5B-Instruct in Colab. The notebook generates 288 synthetic examples, with 192 for training, 48 for validation, and 48 for testing. I assigned related wording variants to the same split by grouping them into authored semantic families. I evaluated the original and fine-tuned versions of the same model on the same held-out cases and examined a separate eight-case challenge suite.
3. **Application.** I integrated the exported checkpoint into a Streamlit prototype. The app checks the approved target vocabulary, required JSON keys, boolean review flag, and rationale before showing a result. The interface records the analyst's decision separately from the model recommendation.

## Results on the 48-case held-out test set

| Measure | Original Qwen | Fine-tuned Qwen |
| --- | ---: | ---: |
| Strictly parsed target accuracy | 4/48 (8.33%) | 41/48 (85.42%) |
| Complete JSON contract | 7/48 (14.58%) | 48/48 (100%) |
| Review recall | 0/9 (0%) | 9/9 (100%) |
| Review precision | Undefined | 9/14 (64.29%) |

Strictly parsed target accuracy counts a correct approved target or `REVIEW` only when the output parses as JSON. The original model produced no review predictions, so its review precision is undefined. The fine-tuned model sent five clear cases to review and chose two wrong destinations. It also missed one required review in the separate challenge suite. The results met the JSON and review-recall thresholds on the main test, while target accuracy and review precision fell short of the notebook's acceptance criteria.

The final application notebook records two live checkpoint checks. `patientDOB` returned `date_of_birth`, and `full_name` returned `REVIEW`. Both passed validation. Four intentionally invalid response examples in the same notebook were routed to review by the response guard.

## Evidence and reproducibility

| Artifact | What to inspect |
| --- | --- |
| [Project proposal](evidence/milestone-1-proposal.pdf) | Problem definition, initial scope, and evaluation plan |
| [Prompt experiment paper](evidence/milestone-2-prompt-experiments.pdf) | Prompt design and results |
| [Prompt experiment notebook](evidence/milestone-2-prompt-experiments.ipynb) and [synthetic CSV](evidence/healthcare_mapping_prompt_experiments.csv) | Six prompt variants, test cases, and saved outputs |
| [Fine-tuning notebook](evidence/milestone-3-fine-tuning.ipynb) | Sections 4–5 for dataset construction and split checks, and Sections 12–14 for results and error analysis |
| [Application verification notebook](evidence/milestone-4-app-verification.ipynb) and [presentation](evidence/milestone-4-presentation.pdf) | Response validation, recorded live inference, and analyst workflow screenshots |

The notebooks contain saved outputs. To rerun the prompt study, place its notebook beside the CSV, use a Python environment with pandas and the OpenAI SDK, and supply `OPENAI_API_KEY` through the environment. API access and charges can apply. To reproduce the tuning run, use a GPU-backed Colab runtime and follow Sections 1–14 in order. The first section installs the recorded Transformers and Accelerate versions, and the notebook generates its own training, validation, and test inputs. The original tuning run used a Tesla T4.

Running the final application requires the original Streamlit project files (including `app.py`, `mapping.py`, and `demo_cases.json`) and the exported model and tokenizer. Place the checkpoint in `final_model/` or use `MAPPING_MODEL_DIR` for the notebook, then run the notebook from the application repository or its immediate notebooks folder. Run `streamlit run app.py` from the application directory to open the interface. This portfolio copy includes the saved evidence. The app source and weights are separate dependencies.

## Limitations and responsible use

All evaluation and demo data are synthetic. The custom target schema covers a limited set of demographic fields. Performance may change with terminology, field conventions, or ambiguous examples from other organizations. The strongest result was reliable JSON on the held-out synthetic test set. The mapping errors still show why an analyst should check the recommendation before using it in a data pipeline. I would next test field metadata from an independently authored benchmark and examine missed reviews and incorrect mappings by source-field type.

## References

- Bahree, A. (2024). *Generative AI in action*. Manning Publications.
- Qwen Team. (2024). *Qwen2.5-0.5B-Instruct* [Model card]. Hugging Face. https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct
- Hugging Face. (n.d.). *Trainer* (Transformers version 4.57.1). https://huggingface.co/docs/transformers/v4.57.1/en/main_classes/trainer
