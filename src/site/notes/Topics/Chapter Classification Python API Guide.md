---
{"dg-publish":true,"permalink":"/topics/chapter-classification-python-api-guide/"}
---


# Documentation Breakdown

## UML Diagrams

All technical documentation can be found under the directory [UML](./UML).

There are provided:

- [.jpg files](./UML/JPGs), diagrams on the project's current state.
- [.drawio files](./UML/DRAWIOs) in case of the need of updating documentation.

## Swagger Endpoint

Information regarding on how to use the endpoints + HTTP actions can be found on the [swagger endpoint](http://127.0.0.1:8000/docs).

## Explanation "/input"s return

Previously "/input" would return a list of the names of every chapter found, without specifying accompanying symptoms.

Whereas, currently:

- The chapter's ID on the database is returned instead of the name of the chapters.
- Classification will only occur to in a safe level of confidence. This is, if it is not clear to which subsubchapter a symptoms belongs, it will not be considered in the classification.
- These are returned in a list. Where, if symptoms are syntatically considered to be related will be gathered in a 'sub-list'.

More on the second change:

| Input                              |                               Classification\*                               |
| ---------------------------------- | :--------------------------------------------------------------------------: |
| I have a headache                  |                  **[** [ "Head, Inner", "Forehead" ] **]**                   |
| I have a headache and my eye hurts |     **[** [ "Head, Inner", "Forehead" ], [ "Eye, Inner", "Orbit" ] **]**     |
| My eye hurts and I have migraine   |     **[** [ "Eye, Inner", "Orbit" ], [ "Head, Inner", "Temples" ] **]**      |
| I have a headache and a migraine   | **[** [ [ "Head, Inner", "Forehead" ], [ "Head, Inner" , "Temples" ] ] **]** |

_\*The database ID would be returned normally instead of the name of the chapter. Here the chapter name is used for visualization purposes_

## Changes to DB structure

If there is ever the need to change the chapter structure in the database it will require to reset the server.

If the server is not reset, there might be unexpected behavior when new training data is given.

## How Naive Bayes works

Given it was requested by Dr. Carl Rudolf to provide the resources used to explain how NB works you may find:

- The .pdf for the [presentation](./PresentationNB.pdf) they were given on Februrary 2024.
- The link to the [video](https://www.youtube.com/watch?v=O2L2Uv9pdDA&ab_channel=StatQuestwithJoshStarmer) that based the presetation.
