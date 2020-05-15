---
layout: post
title: Active Learning Brief Introduction
---
Active Learn introduction.

## Why?

In some case, it is very expensive to label samples, or labels are extremely unbalance. E.g. risk control.

Active Learning can reduce label cost campared with random samples labeling.

## How?

1. Random sampling.
2. Label samples, train model.
3. Predict, get middle samples (score is round 0.5).
3. repeat 2 and 3 until label resource is spent or model is enough good or samples can not be labeled.

## Diffcults

Don't use Active Learning in Financial case becuase bad samples are very sensitive to profit.

Internet case can use Active Learning. E.g. CV and NLP