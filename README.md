# LLM Model Weight Statistical Review

## Report and JSON Links

There is a (very long) by layer report as HTML and a JSON version of the data.

- [Llama 3 8b Report](https://htmlpreview.github.io/?https://raw.githubusercontent.com/cyrusradfar/llm-model-review/main/llama-3-8b/report.html), [json data](./llama-3-8b/metrics.json)
- [Llama 2 7b Report](https://htmlpreview.github.io/?https://raw.githubusercontent.com/cyrusradfar/llm-model-review/main/llama-2-7b/report.html), [json data](./llama-2-7b/metrics.json)
- [Vicuna 13b Report](https://htmlpreview.github.io/?https://raw.githubusercontent.com/cyrusradfar/llm-model-review/main/vicuna-13b/report.html), [json data](./vicuna-13b/metrics.json)

## Processing
To generate the report, a process iterates and analyzes the weights. At each layer the following data is calculated:

 - statistics: mean, median, std dev, max, min
 - frequency histogram with 16 buckets
 - best fitting kmeans clustering by silhouette score, cluster centers included. Examined 3 - 32 cluster counts. Note that a stratified sample across 10 deciles of 1500 weights was used to expedite kmeans clustering

As each layer was processed, the stratified subsamples were aggregated and are called the "FINAL SAMPLE" layer near the end of the report.

The "FINAL STATS" arrays at the very end of the report is pre-aggregated statistics from every layer to simplify any analysis that would go across, e.g. "Maximum max" across all the layers.

## Data Definitions

 - `shape` the dimensions of the tenor, e.g.	`(128256, 4096)`
 - `cluster_calc_time_sec`	the time it took in seconds to find the best kmeans clustering, testing 3 - 32 exclusive, e.g. `1`
 - `count_nonzero`	count of non-zero weights, e.g. `525336576`
 - `zeros` count of zero weights, e.g. `10`
 - `count`	total count of weights (aka parameter count), e.g. `525336576`
 - `zero_percent` percent of zero weights to four sig figs, e.g.	`0.0000`
 - `min` minimum weight (census), e.g.	`-0.08203125`
 - `max` maximum weight (census), e.g. `0.22558594`
 - `mean` average weight (census), e.g. `1.8423598e-05`
 - `median` median weight (census), e.g. `2.646978e-23`
 - `std_dev` standard deviation (census), e.g.	`0.009330472`
 - `freq_table` object containing `freq` (frequency) and `value` (bucket value) -- always 16 buckets. In HTML the table includes an index column. 
 - `best_n_clusters` selected best kmeans clustering N (from 3 - 32 exclusive) using a stratified sample, e.g. `21`
 - `best_cluster_centers` cluster centers as determined by kmeans for the best cluster N
 - `best_silhouette_score` best silhouttete score across kmeans experiments, e.g.	`0.54720515`
 - `best_cluster_boundaries` cluster boundaries from -inf to +inf 

