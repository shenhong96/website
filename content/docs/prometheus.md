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

Metrics can be of different types, and I've tried to wrap my head around each:

### Labels, Filters & Modifiers

Navigating the metrics using labels and filters was an interesting exercise. The modifiers are something I need to delve deeper into.

### Operators: This Seems Like Math!

Operators play a vital role in formulating queries. The more I understand them, the more I can ask of my data.

## Trying Out Some Queries

While exploring, I tried monitoring different Kubernetes pods and formulated some queries. It's fascinating how much data one can extract with the right queries.

I also stumbled upon [PromLens](https://promlens.com), an alternative Prometheus UI. It looks like a great tool for framing complex query syntax.

## Wrapping Up

This is just the beginning of my journey with PromQL. As I venture further, I'll continue to document my learnings. I hope this post offers some guidance to those who, like me, are trying to grasp the intricacies of PromQL. If you have insights or corrections, please share. We're all learners here!

