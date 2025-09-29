# lak26-appendix
Anonymous Appendix for an LAK26 submission

We aim to use LLM to assist users in determining if a tutor's response is effective praise. By providing **guidelines for Giving Effective Praise** and some selected examples as the prompt, we enable the LLM to evaluate whether the tutor's response meets the criteria for effective praise. Additionally, we ask the LLM to generate two explanations for its decision:

1. **Direct text reasoning** for the decision.  
2. **Highlighted input**: the original input with HTML tags marking the sections it deems to meet the standards of effective praise.

Due to length constraints, the full prompt and example output are available at [this gist](https://gist.github.com/anonymousStars/4a56d304515046d806eee4bbfb4d7e2b).

---

We used this prompt to evaluate all models in [Table 1](#tab-models-performance-app). The best accuracy of **0.884** was achieved by *gpt-4-0613*, with an F1 Score of **0.918**.  

Moreover, we performed a majority vote ensemble across models. Combining the following three models improved performance further:

- *gpt-4o-2024-11-20*  
- *gpt-4-0613*  
- *gpt-4-1106-preview*  

This ensemble raised the **Accuracy** to **0.889** and the **F1 Score** to **0.924**.


### Table 1. Development performance of candidate models (used for selection)

| Model                        | Accuracy | Precision | Recall | F1 Score |
|------------------------------|----------|-----------|--------|----------|
| gpt-4o-2024-11-20            | 0.847    | 0.930     | 0.852  | 0.889    |
| gpt-4o-2024-08-06            | 0.847    | 0.918     | 0.865  | 0.890    |
| gpt-4o-mini-2024-07-18       | 0.815    | 0.908     | 0.826  | 0.865    |
| gpt-4-1106-preview           | 0.870    | 0.885     | 0.942  | 0.912    |
| gpt-4-0125-preview           | 0.861    | 0.879     | 0.935  | 0.906    |
| **gpt-4-0613 👑**               | **0.884**| **0.892** | **0.955** | **0.922** |
| gpt-3.5-turbo                | 0.792    | 0.917     | 0.781  | 0.843    |

<a name="tab-models-performance-app"></a>


---

We also conducted an ablation analysis of the prompt using *gpt-4o-2024-08-06*. Results (see [Table 2](#tab-ablate-app)) indicate that **few-shot learning** plays a more significant role than instructions in this context. However, instructions still help by providing additional knowledge that enhances model reasoning and highlighting explanations, as observed in the outputs.

### Table 2. Prompt ablation with *gpt-4o-2024-08-06*

| Few-shot | Instruction | Accuracy | Precision | Recall | F1 Score |
|----------|-------------|----------|-----------|--------|----------|
| X        | O           | 0.653    | 0.976     | 0.529  | 0.686    |
| O        | X           | 0.824    | 0.820     | 0.968  | 0.888    |
| O        | O           | 0.847    | 0.912     | 0.871  | 0.891    |

<a name="tab-ablate-app"></a>
