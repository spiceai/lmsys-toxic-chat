# ToxicChat prompt screening
[ToxicChat](https://huggingface.co/datasets/lmsys/toxic-chat) is a set of real user prompts to a chatbot (the Vicuna demo), with human labels for `toxicity` and `jailbreaking`. Only about 7% of the prompts are toxic, and the jailbreak attempts are a subset of the toxic prompts.

In this spice app, the decision model `jev` screens each prompt before it would reach a chatbot. One `ai_decide` call per prompt asks two questions: is it toxic, and is it a jailbreak attempt. 

The results can be queried in SQL
```sql
-- The 10 prompts jev rates most likely to be jailbreak attempts.
SELECT prompt, p_toxic, p_jailbreak FROM top_jailbreaks;

-- jev precision and recall against the human labels, at a 0.5 threshold.
SELECT label, answered FROM evaluation where label!=answered;
```
