# Lean Six Sigma Process Improvement

## Overview
This project applies the Lean Six Sigma principles in order to improve the efficiency, as well as consistency, of a homemade crispy potato cooking process. Over numerous cooking experiemnts, different times of each step were recorded, bottlenecks were identified, and numerous workflow changes were tested in order to prevent any time being wasted, yet still maintaining product quality. [Crispy Potato Process Improvement Study](https://docs.google.com/document/d/1tb1OeYlXa7Y0CAgNTzawOH31alYT59FleFeqDLf_ZDg/edit?tab=t.0#heading=h.6k8snmjjkkvo)

## DMAIC
### Define
The original cooking process was inconsistent. Numerous problems included excessive frying time, larger batches requiring significantly more time, limited equipment capacity, and an inconsistent workflow between cooking sessions. Earlier attempts also produced potatoes that were often soggy, overly oily, and lacked consistent crispiness, demonstrating the need for a more standardized process.

### Measure
A time study was conducted across twelve cooking experiments. Each trial recorded the duration of every major process step to establish a baseline, compare process variation, and identify where the greatest amount of time was being spent.

Steps:
- Peeling
- Cutting
- Soaking in Salt Water
- Drying
- Vinegar-Water Boiling
- Final Drying
- Frying

### Analyze

When comparring all twelve cooking logs, there were numerous recurring problems.

The frying stage took the longest time, becoming the primary bottleneck. Having larger potato batches didn't help either, mainly because of the oil temperature recovering slower. It didn't help with the equipment limitations involved, mainly because of the fact I used smaller cooking pots, which hampered the process efficiency.

Additional observations also showed that organizing preparation steps and maintaining a consistent workflow helped reduce unnecessary waiting between stages.

### Improve

Several process improvements were tested throughout the twelve cooking experiments.

These improvements included:

- Limiting potato batches to improve frying efficiency.
- Preheating the cooking oil before frying.
- Using a larger cooking pot to prevent overcrowding.
- Standardizing drying procedures before frying.
- Experimenting with vinegar-water cooking times.
- Refining preparation workflow to reduce idle time between process steps.

Each experiment built upon observations from previous trials to gradually improve process consistency.

### Control

The final process recommendations help maintain consistent product quality while reducing unnecessary cooking time.

Recommended standard practices include:

- Limit each batch to two or three potatoes.
- Always preheat the oil before frying.
- Use a sufficiently large cooking pot.
- Maintain consistent drying times before frying.
- Follow the standardized cooking workflow developed throughout the study.

These recommendations reduce process variation while improving consistency and minimizing wasted energy.

## Key Results

- 12 documented cooking experiments
- Complete time study of every major process step
- Identified frying as the primary process bottleneck
- Developed standardized cooking workflow
- Reduced unnecessary energy usage by recommending smaller batch sizes
- Applied Lean Six Sigma DMAIC methodology to a real-world process

## MOST Analysis

The crispy potato process was evaluated from a work measurement perspective using MOST (Maynard Operation Sequence Technique).

Although a complete MOST time standard was not developed for this project, several manual tasks were identified as candidates for future analysis, including:

- Peeling potatoes
- Cutting potatoes into uniform strips
- Moving potatoes between soaking, drying, and boiling stages
- Loading and unloading potatoes from the frying pot
- Organizing tools and workspace during preparation

A future MOST analysis could establish standard times for each manual operation, identify unnecessary motions, and further reduce overall process time through improved work methods.

## Process Maps
Coming soon...

## Process Maps

The cooking process was organized into three major phases: **Preparation**, **Cooking**, and **Continuous Improvement**. Separating the workflow into phases made the process easier to analyze and helped identify where delays occurred.

```mermaid
flowchart LR

    A([Start])

    subgraph P[Preparation]
        B[Gather Ingredients] --> C[Peel Potatoes] --> D[Cut Potatoes] --> E[Soak in Salt Water] --> F[Dry Potatoes]
    end

    subgraph CKG[Cooking]
        G[Boil in Vinegar Water] --> H[Final Drying] --> I[Preheat Canola Oil] --> J[Fry Potatoes]
    end

    subgraph CI[Continuous Improvement]
        K[Taste & Evaluate Quality] --> L[Record Times & Observations] --> M[Compare with Previous Logs] --> N[Adjust Process for Next Trial]
    end

    A --> B
    F --> G
    J --> K
    N --> O([End])
```
