# response-model

Classification models for determining if a message was responded to in online forums. 
The models aim to predict whether a given message was responded to by another user.
The target feature label is `replied`.

This repository tests the following models:

| Model | Description                                                    |
|-------|----------------------------------------------------------------|
| BERT  | Bidirectional encoder representations from transformers (BERT) |

## Project Structure
```
response-model/
│
├── src/
│   ├── experiments/
│   ├── ml/
│   ├── tasks/
│   └── pipelines/
│
├── models/
│
├── data/
│
└── README.md
```

## Input Schema
| Feature       | Data Type | Description                                                               |
|---------------|-----------|---------------------------------------------------------------------------|
| is_op         | bool      | Indicates whether this message is the subject of the conversation/thread  |
| thread        | integer   | The unique identifier of the thread that the conversation took place      |
| post_id       | integer   | The unique identifier of the message that was posted                      |
| time          | integer   | The time that the message was posted                                      |
| replied       | bool      | Indicates that the message was replied to by another user                 |
| content       | string    | The content of the post                                                   |

## Training Pipeline
To train each of these models, the input schema must go through the following:
1. All features must be cast to the correct data types.
2. Content field is tokenized to be N features. 
3. Content tokens that are shorter than N features are padded, and tokens that are longer are concatenated.
4. The dataset is split into training and testing sets.
5. A model is trained and the weights are saved to the models/ directory.