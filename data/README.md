# Homework 1 dataset - Event Detection

As explained in the other material you received, in this homework you will have to carry out an Event Detection task.
You are asked to detect which words in a sentence represent the event trigger, and what type of event they indicate.

## Event schema

Each event can be part of one of the following classes: Sentiment, Scenario, Change, Possession, Action.

We adopt the IOB tagging scheme, introduced by Ramshaw & Marcus (1995), to label each token of the dataset.
Each token can have one of the 11 tags presented in the "IOB label tags" column of the table below.


| Event class | IOB label tags               | 
|:------------|:-----------------------------|
| Sentiment   | `B-SENTIMENT, I-SENTIMENT`   |
| Scenario    | `B-SCENARIO, I-SCENARIO`     |
| Change      | `B-CHANGE, I-CHANGE`         |
| Possession  | `B-POSESSION, I-POSESSION` |
| Action      | `B-ACTION, I-ACTION`         |
| -           | `O`                          |

A label prefixed with `B-` ("begin") indicates that the corresponding token is the first of an event trigger with the given class.
If the event trigger is composed of multiple tokens, the following labels of the event trigger will be prefixed with `I-` ("inside").
If the token is not part of an event trigger, it will be labelled with `O` ("outside").

## Data schema

You will be given three JSONL files, `train.jsonl`, `dev.jsonl` and `test.jsonl` which contain respectively 20,000, 2,000 and 2,000 sentences.
Each line in any of the three files is a JSON object with three fields:
- `idx`: progressive index of the sample, unique to each split.
- `tokens`: The pre-tokenized sentence, i.e. a list of tokens that make up the sentence.
- `labels`: A list with the same length of `tokens`, with the corresponding label for each token.

Here is a practical example from the training set:
```json
{
    "idx": 134, 
    "tokens": [
        "The", "cyclone", "passed", "very", "close", "to", "the", "Vanuatu", "capital", "city", "of", "Port", "Vila", ",", "forcing", "the", "evacuation", "of", "about", "2,000", "people", "and", "shutting", "down", "the", "main", "port", "."
    ], 
    "labels": [
        "O", "O", "B-Action", "O", "O", "O", "O", "O", "O", "O", "O", "O", "O", "O", "B-Change", "O", "O", "O", "O", "O", "O", "O", "B-Change", "I-Change", "O", "O", "O", "O"
    ]
}
```

## References
[Text Chunking using Transformation-Based Learning](https://aclanthology.org/W95-0107) (Ramshaw & Marcus, VLC-WS 1995)

