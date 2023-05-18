# Metrics

_Source: [https://www.youtube.com/watch?v=czes-oa0yik](https://www.youtube.com/watch?v=czes-oa0yik)_

## Why should we care about Metrics?

As a Software Engineer, your job is to generate business value. You generate business value by making well-informed decisions.

Remember that a map ≠ territory, i.e., the map of Toronto is not the reality of Toronto. In the same way, our mental model and perception are not necessarily the same as reality.

We have a mental model of what our code does, but unless we measure it in production, we don't know what the reality is. Metrics allow us to make better decisions, generating more business value.

## Our Toolkit

### Gauge

An instantaneous value of something.

Example: A total size of some resource, e.g., 1600 users registered.

### Counter

An incrementing and decrementing value.

Example: Increment a value when a user connects, decrement when they disconnect to store the current online users count.

### Meter

An average rate of events over a period of time.

Example: We dropped from 5000 requests/sec to less than 200 requests/sec.

Additional: We care about recency! These rates should be the exponentially weighted moving average.

### Histogram

A statistical distribution of values in a stream of data.

We want to measure quantiles, median, 75, 95, 98, 99, 99.9th percentile.

Additional: We can't possibly store every single event and then sample from it to get our percentiles, and recency matters, so we use forward-decaying priority sampling. This allows us to maintain a statistically representative sample while keeping a small sample size for space efficiency over, e.g., the last X minutes.

Example: 95% of the autocomplete results return 3 words or less.

### Timers

A histogram of durations and a meter of calls.

Timers are a compound metric. Not just about throughput but also the latency and its distribution.

Example: At ~2000 req/s, our 99% latency jumps from 13ms to 554ms.

## Use the Toolkit

1. **Instrument it.** If it could affect your code's business value, add a metric.
2. **Collect it.** Use a service to collect metrics reported by services.
3. **Monitor it.** Use a tool to monitor the data that's collected. Set up alarms and page alerts.
4. **Aggregate it.** Get insights and historical context into your services.

## Shorten Decision Making Cycle with the OODA Model

1. **Observe**
   
   Question: What is the 99% latency of our autocomplete service right now?  
   Answer: ~500ms

2.  **Orient**

   Question: How does this compare with other parts of our system both currently and historically?  
   Answer: Very slow compared to other services

3. **Decide**
   
   Question: Should we make it faster? Or should we add a new feature?  
   Answer: We gain more business value from making it fast!

4. **Act**
   
   Decision: Write some code and fix the bottlenecks!  

Faster decision making means: our mistakes won't live as long, and we will ship more impactful features.

## tl;dr

In order to know how well our code is generating business value, we need metrics.
