---
layout: page
title: Spend Analytics Visuals <a href='https://github.com/eleanorfleming96/Portfolio/blob/main/Spend_Data_Visualization.ipynb' target='_blank'>[GitHub]</a>
permalink: /spend-analytics-visuals/
---

>Throughout 2024 at <a href="https://www.airflip.com" target="_blank">Airflip</a>, I prototyped spend analytics charts and dashboards using Python and Metabase to support engineering implementation. These charts are designed to help procurement teams effectively investigate their company's spend data. Below are a few example prototypes that were incorporated into our platform.
>
>
These examples use a coffee shop's spend data across various categories (Level 1 - 3) such as inventory, supplies, and equipment. 
>

### Pareto Analysis ###

A Pareto chart ranks spending categories from highest to lowest, highlighting which areas most impact total expenditures and their cumulative contribution (blue bars for absolute spend, red line for cumulative percentage). Labor and Rent & Lease dominate, showing that a few categories account for the majority of costs. 

<iframe src="{{ site.baseurl }}/public/charts/pareto_level_1_category.html" width="100%" height="600" frameborder="0"></iframe>


This reflects the 80/20 principle in procurement, where targeting categories that make up around 80% of total spend can achieve significant cost savings. This type of analysis helps teams prioritize their spend strategies by focusing on the most important cost drivers.

### Treemap ###

<iframe src="{{ site.baseurl }}/public/charts/treemap.html" width="100%" height="600" frameborder="0"></iframe>

This treemap visually illustrates the coffee shop’s spending hierarchy by sizing each rectangle according to the relative amount spent (logarithmic scale to improve readability). The larger and darker blue rectangles, like Labor and Rent & Lease, immediately convey the biggest cost drivers. Within each top-level category, subcategories can be expanded to show how smaller costs add up within the broader spend areas. 

### Sankey ###

<iframe src="{{ site.baseurl }}/public/charts/coffee_shop_sankey.html" width="100%" height="600" frameborder="0"></iframe>

A Sankey diagram shows how a total (in this case, the coffee shop’s spending) flows through multiple categories, with the width of each flow indicating its relative size. It’s particularly useful for highlighting where the bulk of costs occur and how they break down across subcategories. For example, the diagram above provides a clear visual of how costs are distributed within the Inventory Level 1 and 2 sub categories.