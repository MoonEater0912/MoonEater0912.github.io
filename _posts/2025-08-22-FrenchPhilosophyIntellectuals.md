---
title: "The Politics of Metaphysics: French Philosophy and Intellectuals in the 20 Century"
date: 2025-08-22
layout: post
category: research
image: "/images/databnf.png"
---

This is the ongoing project related with my master thesis. I am still working on the data collecting and preliminary exploration, supervised by Jacob Habinek.

Text data was requested from [JSTOR](https://www.jstor.org). I selected 5 most typical traditional philosophy journals in french (founded in France before WWII, and still active into the 1990s): 
- Archives de Philosophie
- Revue de Métaphysique et de Morale
- Revue de Théologie et de Philosophie
- Revue des Sciences Philosophiques et Théologiques
- Revue Internationale de Philosophie

I kept the authors having at least 2 publication recordings during 1950 - 1989 as samples. After cleaning and normalizing authors' names (really a HUGE task), I collected author metadata (gender, nationality, birth/death year/place, employer/institution) from [WikiData](https://www.wikidata.org/wiki/Wikidata:Main_Page) and [BNF](https://data.bnf.fr), using Python.

I plan to analyze the dataset from 3 layers:
- Population layer: analyzing biographical and institutional data
- Document layer: looking at the semantic and topic transform through the 40 years, especially the comparion of before and after 1968
- Intersection layer: dynamically mapping the conceptual relevance network with authors' social space positions