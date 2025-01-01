---
layout: post
title: Causal Inference V2
---

风控背景读因果推断 - 个人总结V2

## 输出是什么，解决什么问题

之前一直对因果推断的输出存疑。即使通过因果推断的手段，证明因素A对结果B有影响（正向影响，甚至影响率或影响公式），这个因果有什么作用呢？这个疑问尤其在风控角度难以解释，例如我们知道比如说地域对授信结果有影响，能做的就是构建一个使用了地域特征的分类模型（或策略）来优化授信流程。这仅对于特征选择有些许影响。这个推断往往通过历史数据和标签就能够分析出来，所谓A/B test，反事实结果，这些大体上都没什么意义。

然而了解了一些营销场景之后，这个疑虑渐渐减少了。营销和风控最大的不同是结果，风控的结果基本就是拦截或者不拦截，而营销的结果不是投放或者不投放，而是投放收益。这就有点像是回归问题了，但也不完全是回归。

在风控中，拦截或者不拦截加上欺诈FN和客诉FP，形成的是典型二分类标签下的指标，准确率和召回率。在营销中，指标本身是一种商业反应，比如月活，利润，转化率等等。而所谓的投放或者不投放，本身是一种干预行为，这种干预是相比风控中的拦截，是能够的到更长链路和种类繁多的反馈的。所以投放或者不投放，更像是了特征，而不是结果。如果以它们和其他background factor为特征，以指标为结果，就是一种回归。可是问题本身不是回归，或者说预测商业指标，而是人们期望以对特征的调整，取得商业指标的正向趋势（来融资上市圈钱或者真正make profit）。所以因果推断这项技术也不是为了解决这种回归问题，而是由于使用分渠道，分人群的投放策略作为了中间产物的原因，出现了同时影响投放和最终指标的混杂特征，因果推断应运而生。

从我的理解看，首先将回归问题简化，形成一个仅靠着投放策略形成的初级线性函数，更优的投放策略直接可以认为是对商业指标有正的影响。然后通过重点研究投放策略的因果，调整这些因，来达到更好的果（投放策略），从而就可以得到更好的商业指标。

此外还有一个点很不一样，就是特征。特征在风控里往往是越做越多的，因为往往更需要拟合各种各样的攻击手段，欺诈方式等。但标签往往是较难获取的。而营销往往是标签，或者说商业指标易于统计，因为这种往往是高度聚合的。特征就需要深挖，需要经验，需要推动开发做埋点，需要梳理底层表。结果就是特征可能越挖越多，可是作为因果推断的结果，输出的可以作为因的特征却往往是更少的。
