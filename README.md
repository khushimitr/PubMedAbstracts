
# PubMed Abstract

This project takes on the problem that the number of RCT (Randomized Controlled Trial)
papers released is continuing to increase, and those, without 
structured abstracts can be hard to read and in turn slow down 
researchers moving through the literature. So we created a NLP 
model to classify abstract sentences into the role they play 
(e.g. objective, methods, results, etc) to enable researchers 
to skim through the literature and dive deeper when necessary.

```
In other words, given the abstract of a RCT, what role does each sentence serve in the abstract?
```

Where our data is coming from: [PubMed 200k RCT: a Dataset for Sequential Sentence Classification in Medical Abstracts](https://arxiv.org/abs/1710.06071)

## Demo

<p align="center">
  <img alt="Input" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/Screenshot_1.png" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Output" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/Screenshot_2.png" width="45%">
</p>

## Methodology

* `Preprocessing` steps involve changing all the numerics to @.
* Get the list of sentences and their labels. 
* `Labels` should be in form of numerics or one hot encoded.
* We used both custom text vectorization layer and Universal Sentence Encoder [(USE)](https://www.tensorflow.org/hub/tutorials/semantic_similarity_with_tf_hub_universal_encoder) to check what performed best.
* Then we conducted various modelling trial on 10% of the data to see which model performed best and we can extend it.

```
Model 0: MultiNomial NaiveBayes (Baseline)
Model 1: CONV 1D with Token Embeddings
Model 2: Feature Extraction with Pretrained Token Embeddings
Model 3: CONV 1D with character Embeddings.
Model 4: MultiModal (Combining Token Embeddings + Character Embeddings)
Model 5: TriBred Model (Combining Token Embeddings, Character Embeddings and Positional Embeddings)
```

For our last model we made `line numbers` and `total lines` also a feature for our sequential model to learn.
This proved to increase our accuracy to 83%. This concept is called [Feature Engineering.](https://towardsdatascience.com/what-is-feature-engineering-importance-tools-and-techniques-for-machine-learning-2080b0269f10#:~:text=Feature%20engineering%20is%20the%20process,design%20and%20train%20better%20features.)

Below is the comparision of the above mentioned models:

<p align="center">
  <img alt="Model Comparision" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/model_compare_20k_rct.png" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="F1 Score Comparision" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/f1_score.png" width="45%">
</p>

Now, we took the best two models and trained them on whole dataset.

These models were:
* Model 1: CONV 1D with Token Embeddings
* Model 5: TriBred Model (Combining Token Embeddings, Character Embeddings and Positional Embeddings)


## Weights
Weights of the two top models trained on whole dataset can be found [here](https://drive.google.com/drive/folders/1-1pO1nFpF3uR9F0RyHlh5FYX7C7_5HWo?usp=sharing).

Below is the layer architecure of both the models:

**Model 1:**

![App ScreenShot](https://github.com/khushimitr/PubMedAbstracts/blob/main/images/Model_1_Conv1D.png)

**Model 2:**

![App ScreenShot](https://github.com/khushimitr/PubMedAbstracts/blob/main/images/model_2_tribrid.png)

## Model
The best performing model which acheives an accuracy of 87% can be found [here](https://drive.google.com/drive/folders/1074IigKywor7jZVaJZLDgxgEJ18C0pai?usp=sharing).

### Loading Model

```
model_path = "PubMed/pubmed_200k_model"
model = tf.keras.models.load_model(model_path,custom_objects={"TextVectorization": TextVectorization,"KerasLayer": hub.KerasLayer})
```

## Run Inferences

* You can either use the json

```
    with open("json_filepath","r") as f:
        doc = json.load(f)
    
    make_predictions(doc[0]["abstract"])
```

* You can also copy paste any abstract

```
    doc = "Your abstract that you wish to skim"
    make_predictions(doc)
```

## Some Example Outputs

<p align="center">
  <img alt="Input" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/Screenshot_3.png" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Output" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/Screenshot_4.png" width="45%">
</p>

<p align="center">
  <img alt="Input" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/Screenshot_5.png" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Output" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/Screenshot_6.png" width="45%">
</p>

