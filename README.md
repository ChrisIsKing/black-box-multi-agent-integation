# One Agent To Rule Them All: Towards Multi-agent Conversational AI

Repository that accompanies [One Agent To Rule Them All: Towards Multi-agent Conversational AI](https://csclarke.com/assets/pdf/ACL_2022.pdf)

### Multi-agent Data
The dataset collected for this paper is located in the `./data` folder and consists of all question-response pairs used for training the MARS encoder and evaluating the `question agents pairing` and `question response pairing` approaches.

### Models
Our trained and evaluated models will be released on HuggingFace in the coming weeks. Additionally, we'll provide a training and test script to reproduce results in the `./models` folder.

The baseline models evaluated in this paper can be accessed here:
- [Universal Sentence Encoder](https://tfhub.dev/google/universal-sentence-encoder/4)
- [Universal Sentence Encoder Question Answering (USE QA)](https://tfhub.dev/google/universal-sentence-encoder-qa/2)
- [Roberta+STS](https://huggingface.co/sentence-transformers/stsb-roberta-base)
- [BM25](https://github.com/dorianbrown/rank_bm25)