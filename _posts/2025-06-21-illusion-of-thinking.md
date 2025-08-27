---
layout: distill
title: Thoughts on "The Illusion of Thinking"
description: My thoughts and some experiments on a recent paper by Apple titled the "Illusion of Thinking"
draft: true
tags:
giscus_comments: false
date: 2025-06-21
featured: false
mermaid:
  enabled: true
  zoomable: true
code_diff: true
map: true
chart:
  chartjs: true
  echarts: true
  vega_lite: true
tikzjax: true
typograms: true
# thumbnail:
# og_image:
# og_image_width: 2126
# og_image_height: 1478
authors:
  - name: Lars Rosenbaum
    url: "https://lcrosenbaum.github.io"
output: distill::distill_article
bibliography: illusion-of-thinking.bib

toc:
  - name: Invariant Geometric GNNs
  - name: Fully Connected Graphs and Transformers
  - name: Alfafold 3 Pairformer
  - name: A different view on Pairformer
  - name: Some Performance Evaluations
  - name: Final Thoughts

_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }
---


## Paper Review

### Summary

The authors of the paper take a look at the reasoning capabilities of the current Large Reasoning Models (Thinking Models, LRMs) trained with reinforcement learning on problems that are verifyable, e.g. math problems or coding challenges. They compare their performance to their non reasoning counterparts (LLMs) on a set of puzzle problems. The main takeaway is that (1) reasoning models perform better with increasing task complexity and (2) that all models break down at high complexity, questioning their stark reasoning capabilities.

LRMs show an increasing performance gain on reasoning benchmarks like MATH500 or the AIME, a challenging mathematics competition for high school students. However, the authors notice that while LRM and LLM performance on AIME 2025 is lower compared to AIME 2024, the students performance is higher. The authros hypothesize possible stronger data contamination in e.g. AIME 2024 benchmarks. This is why the authors suggest scalable puzzle environments as basis for benchmarking, where complexity can be easily scaled and evaluated via simulators, e.g. Tower of Hanoi or River Crossing puzzles.

For all puzzle environments the authors can identifiy three regimes: low, medium, and high complexity. For low complexity, both LLMs and LRMs perform well. At medium complexity there is a gap between thinking models (LRMs) and non-thinking models (LLMs). At high complexity, all models break down to zero performance (see Fig 1. for original results). This breakdown also happens, if the solution algorithm is provided to the model and it happens well before the token budget is used up. It is also observed that at low complexity, the non-thinking models actually need a lower token budget and are more efficient.

<div class="iot_figure4">
  {% include figure.liquid path="assets/img/illusion-of-thinking/illusion-of-thinking-Figure4.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  <div id="fig1" class="caption" style="text-align: left;">Fig. 1 Illusion of thinking results (Figure 4 in paper) showing performance of Claude Sonnet 3.7 and DeepSeek models (thinking and non-thinking) for puzzle environments. Yellow, blue, and red regions indicate the complexity regimes low, medium, and high, respectively.</div>
</div>

The authors also explore the partial solutions provided within the thinking tags of the models. Fig. 2 shows the original results of the paper. For the Tower of Hanoi puzzle (easiest puzzle) the thinking models tend to find correct solutions early in the chain, but then overthink and produce a wrong intermediate solution. In the paper they mention this as a general finding, but as shown in the figure, this can only be observed for the Hanoi puzzle.

<div class="iot_figure7">
  {% include figure.liquid path="assets/img/illusion-of-thinking/illusion-of-thinking-Figure7.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  <div id="fig2" class="caption" style="text-align: left;">Fig. 2 Illusion of thinking results (Figure 7 in paper) showing position of correct solution within thinking tags normalized by thinking length for the four puzzle environments and different complexities.</div>
</div>

### Critical Analysis

The first criticism is with respect to using the Tower of Hanoi puzzle environment. To me this feels not really like complexity, but the algorithm is quite simple and can be solved via induction. The number of moves necessary is $$2^N -1$$, where $$N$$ is the complexity of the puzzle. Checking the default output format of "moves" we need around 7 tokens per move. This means that for $$N=10$$, $$(2^N - 1)*7 = 7161$$ tokens for the output. For $N=12$ already 28665 tokens are required. So the Tower of Hanoi is simply a token battle and has not much to do with thinking.

## Paper Review



## Appendix

### Move Complexity Tower of Hanoi