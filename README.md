> Please change the path directories accordingly in each file.
# Initial Finetuning the model
1. Download data using the code provided by the host.
2. Preprocess train data `preprocess_train.py`
3. Creating JSON for finetuning using LLaMA-Factory `dataprep.py`
4. Follow guidelines given in docs of LLaMA-Factory to register our dataset.
5. For finetuning follow `finetune.ipynb`. Settings for finetuning will registered using WebUI.

# Inferencing of Finetuned Model
1. Run `inference.py`
2. Evaluation Metric: F1 Score

# Experimentation

```yaml
    1. Inference Baseline Qwen2VL-7B-Instruct AWQ
        score: 0.617
        prompt: <Return only value>What is the {entity_name} of this product?

    2. Finetuning
        prompt: What is the {entity_name}?
        a. 10k Samples
            postprocessing:
                a.Replaced Range with NA:
                    - Invalid units replaced with NA
                    - score: 0.678
                b.Replaced range with Max Value:
                    - score: 0.677

        b. 20k Samples with Cosine Scheduler
            Inference Results:
                - score: 0.679
            FineTuned - Curated 1600 samples:
                - score: 0.865
                - lr_scheduler: reduce-lr-on-plateau
                
            FineTuned on 20k samples:
                - score: 
                - lr_scheduler: reduce-lr-on-plateau
                - Preprocessing: 
                    - Replace Range with Max value
                    - Remove entity values with invalid units
                    
    3. Data Curation
        - Missing {entity_value} replaced with NA
        - Correct inaccurate {entity_value}
    
    4. Experimental Settings
        -- batch_size: 8
        -- learning_rate: 5e-5
        -- gradient_accumulation: 8
        -- scheduler: appropriately choosen
        -- tool: LLaMA-Factory
        -- finetuning method: qlora-8bit
        
```
# AMLChallenge
# AMLChallenge
