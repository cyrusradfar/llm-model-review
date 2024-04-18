# LLM Model Weight Statistical Review

## Report and JSON Links

There is a (very long) by layer report as HTML and a JSON version of the data.

- [Llama 3 8b Report](https://htmlpreview.github.io/?https://raw.githubusercontent.com/cyrusradfar/llm-model-review/main/llama-3/report.html), [json data](./llama-3/metrics.json)
- [Llama 2 7b Report](https://htmlpreview.github.io/?https://raw.githubusercontent.com/cyrusradfar/llm-model-review/main/llama-2-7b/report.html), [json data](./llama-2-7b/metrics.json)
- [Vicuna 13b Report](https://htmlpreview.github.io/?https://raw.githubusercontent.com/cyrusradfar/llm-model-review/main/vicuna-13b/report.html), [json data](./vicuna-13b/metrics.json)

## Processing
To generate the report, a process iterates and analyzes the weights. At each layer the following data is calculated:

 - statistics: mean, median, std dev, max, min
 - frequency histogram with 16 buckets
 - best fitting kmeans clustering by silhouette score, cluster centers included. Examined 3 - 32 cluster counts. Note that a stratified sample across 10 deciles of 1500 weights was used to expedite kmeans clustering

As each layer was processed, the stratified subsamples were aggregated and are called the "ALL" layer at the end of the report.

