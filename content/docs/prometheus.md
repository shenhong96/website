+++
title = 'My Journey into PromQL: Exploration'
date = 2022-12-23T15:53:19+08:00
draft = false
+++

# My Journey into PromQL: A Beginner's Exploration

Recently, I embarked on a journey to understand PromQL, the query language for Prometheus. The experience felt akin to learning a new language: exciting, challenging, and sometimes overwhelming. I've decided to document my findings as a way to solidify my understanding, hoping it might help fellow beginners. Remember, I'm still new to this, so there might be nuances I've missed. Feel free to share any insights or corrections!

## What I Understand About PromQL So Far

PromQL is Prometheus's query language. At its core, it seems designed to help users extract meaningful data from their monitoring metrics. Here's what I've gathered:

### Metric Types: Starting Simple

Metrics seem fundamental in any monitoring system. From what I've seen, in PromQL, they can be of various types:

- **String**: Appears to be a textual representation.
- **Scalar**: Seems to be straightforward numeric values.
- **Range Vector**: From what I can tell, it's a combo of multiple values.
- **Instant Vector**: My understanding is that it's like a snapshot of data at a particular moment.

### Grasping Data Types
1. **Counter**: Metrics that get increase over time  *eg: error count, http count*
    - `rate(http_request_count [5s])`
    - Tips: When creating a dashboard, if you query the metrics section using the keyword "total", the metrics that appear are typically viewed as counter elements, which tend to accumulate over time.
2. **Gauge**: Unlike counters, gauges can fluctuate. I think of it like a speedometer.
    - `avg_over_time(http_response_time[5ms])`
    - Tips: Do not use "rate" for Gauge!
3. **Histogram**: This seems useful for averages and percentiles, storing aggregated metrics.
    - `rate(metric_duration_sum[5m]) / rate(request_duration_count[5m]) = avg`
    - predefine function to calculate percentile
        - `histogram_quantile (0.95, sum(rate(request_duration_bucket[5m])) by (le))`
        - `histogram_quantile (0.95, sum(rate(etcd_lease_object_counts_bucket[5m])) by (le))`
    - Tips: Query metrics section using keyword "bucket".
4. **Summary**: It seems to collect a lot of measurements and provides average percentiles.

Metrics can be of different types, and I've tried to wrap my head around each:

### Labels, Filters & Modifiers
1. **Labels** can be equated to (`=`), not equated to (`!=`), matched positively with regex (`=~`), or negatively (`!-`).
    - Tips: When using regex, it's better to make sure the query returns something, eg:
        - Bad example: `http_requests_total{job=~".*"}`  *possible that it matches nothing*
        - Good example: `http_requests_total{job=~".+"}` *we makesure that at least 1 is return*
2. **Ranges** define the time duration, with units like seconds (`s`), minutes (`m`), or hours (`h`).
3. **Modifiers** seem a bit advanced. One I managed to grasp is `rate(http_requests total[5m] @1609746000)` where `@` in this case is the modifier where we modified the exact timestamp to retrieve that data.

Navigating the metrics using labels and filters was an interesting exercise. The modifiers are something I need to delve deeper into.

### Operators: This Seems Like Math!
1. **Aggregation**: This seems to summarize data.
    a. only used instant vector as input, and it will output instant vector as well
	b. aggregation (<instant_vector>) => <instant_vector>
	c. eg: `sum, min, max, stddev, avg, quantile`
2. **Binary**: Basic mathematical operations.
    a. `^`
	b. `*, /, %`
	c. `+, -`
	d. `==, !=, <=, <, >=, >`
	e. `and, or, unless`
3. **Functions**: Predefined operations applied to metrics.
    a. `rate(<instant_vector>) => <instant_vector>`  rate is the function.
Operators play a vital role in formulating queries. The more I understand them, the more I can ask of my data.

## Wrapping Up

This is just the beginning of my journey with PromQL. As I venture further, I'll continue to document my learnings. I hope this post offers some guidance to those who, like me, are trying to grasp the intricacies of PromQL. If you have insights or corrections, please share. We're all learners here!

I also stumbled upon [PromLens](https://promlens.com), an alternative Prometheus UI. It looks like a great tool for framing complex query syntax.

