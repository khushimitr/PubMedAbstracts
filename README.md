# PubMed Abstract

This project takes on the problem that the number of RCT 
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
    <div style="width: 33%; float: left">
        <h3>Abstract (Harder to read)</h3>
        <img alt="Balasana" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/Screenshot_1.png" width="45%">
    </div>
    &nbsp; &nbsp; &nbsp; &nbsp;
    <div style="width: 33%; float: left">
        <h3>Skimmable Abstract(Easier to Read)</h3>
        <img alt="Balasana" src="https://github.com/khushimitr/PubMedAbstracts/blob/main/images/Screenshot_2.png" width="45%">
    </div>
</p>
