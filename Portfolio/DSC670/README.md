# Healthcare Data Mapping Assistant

**Shelia Howard · DSC670 Advanced Uses of Generative AI · Bellevue University**

I built a Streamlit prototype that helps healthcare data analysts map incoming patient and member demographic fields to a shared schema. The analyst enters a source field name, datatype, description, and optional synthetic example value. The app recommends one of 13 approved target fields or returns `REVIEW` for analyst attention. It displays the rationale and records the analyst’s decision separately from the model’s recommendation.

## Project scope

A field such as `patientDOB` can map directly to `date_of_birth`. A field containing a full legal name requires review because the target schema stores given and family names separately. The project covers demographic fields such as identifiers, names, dates of birth, administrative sex, addresses, and contact information.

## Data and approach

1. **Prompt design.** I authored a 30-row synthetic metadata dataset and compared six GPT-4o mini prompt variants on the same six cases, which included three direct mappings and three ambiguous cases. Adding an explicit review option improved target accuracy from 3/6 with the controlled-schema prompt to 5/6 with the explicit review prompt. The exercise informed the target schema and JSON response requirements.
2. **Model fine-tuning.** I fully fine-tuned Qwen2.5-0.5B-Instruct using Hugging Face Transformers in Google Colab. The notebook generated 192 synthetic training examples, 48 validation examples, and 48 held-out test examples. Related wording variants stayed in the same split to reduce leakage. I evaluated the original and fine-tuned models on the same held-out test set and examined a separate eight-case challenge set.
3. **Application and validation.** I integrated the exported checkpoint into Streamlit. The app checks the target vocabulary, required JSON keys, boolean review flag, and rationale. Analysts can accept, revise, reject, or hold a recommendation and export their decision as JSON.

## Results

| Measure on the 48-case held-out test set | Original model | Fine-tuned model |
| ---------------------------------------- | -------------: | ---------------: |
| Strictly parsed target accuracy          |   4/48 (8.33%) |   41/48 (85.42%) |
| Complete JSON contract                   |  7/48 (14.58%) |     48/48 (100%) |
| Review recall                            |       0/9 (0%) |       9/9 (100%) |

Strictly parsed target accuracy gives credit when the response parses as JSON and the target or `REVIEW` decision matches the reference answer. The fine-tuned model’s review precision was 9/14 (64.29%).

In the Milestone 4 verification notebook, the live checkpoint mapped `patientDOB` to `date_of_birth` and returned `REVIEW` for `full_name`. Both responses passed validation. The validator also routed all four deliberately invalid responses to review.

## Project files

| Artifact                                           | Contents                                                                               |
| -------------------------------------------------- | -------------------------------------------------------------------------------------- |
| Project proposal                                   | Problem definition, scope, and evaluation plan                                         |
| Prompt experiment paper and notebook               | Prompt variants, synthetic test cases, and saved outputs                               |
| Fine-tuning notebook                               | Dataset generation, split checks, model training, and evaluation                       |
| `app.py` and `mapping.py`                          | Streamlit interface and mapping logic                                                  |
| `demo_cases.json`                                  | Two synthetic demonstration cases                                                      |
| Application verification notebook and presentation | Saved live inference results, response checks, and screenshots of the analyst workflow |

## Run the application

Use Python 3.11 and open a terminal in the application directory, where `app.py` and `mapping.py` are located.

1. Install the live inference dependencies.

   ```sh
   python -m pip install -r requirements-model.txt
   ```

2. Download the [saved model checkpoint](https://drive.google.com/drive/folders/1EkUaVpxS2ZVONOwtCsXjqKF7wtf-c9tJ?usp=drive_link). Access is restricted to authorized reviewers. Extract the model ZIP so that `config.json`, the tokenizer files, and the model weights sit directly inside `final_model/` beside `app.py`. You can also set `MAPPING_MODEL_DIR` to the directory containing the extracted files.
3. Start the app.

   ```sh
   python -m streamlit run app.py
   ```

4. Open `http://localhost:8501`, select **Live Qwen checkpoint**, and enter synthetic field metadata. Try `patientDOB` with datatype `date` and description “Patient date of birth.” Then try `full_name` with datatype `string` and description “Full legal name in one field.”

For the illustrative two-case demo, install `requirements.txt` and use the same Streamlit launch command.

## Scope of the results

The evaluation and demonstration used synthetic data and a target schema limited to demographic fields. The results measure performance on those cases. An analyst should verify proposed mappings before using them in a data pipeline.

## References

- Bahree, A. (2024). *Generative AI in action*. Manning Publications.
- Qwen Team. (2024). [*Qwen2.5-0.5B-Instruct*](https://huggingface.co/Qwen/Qwen2.5-0.5B-Instruct) [Model card]. Hugging Face.
- Hugging Face. (n.d.). [*Trainer*](https://huggingface.co/docs/transformers/v4.57.1/en/main_classes/trainer) (Transformers version 4.57.1).
