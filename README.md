# One Agent To Rule Them All: Towards Multi-agent Conversational AI
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/one-agent-to-rule-them-all-towards-multi-1/multi-agent-integration-on-bbai-dataset)](https://paperswithcode.com/sota/multi-agent-integration-on-bbai-dataset?p=one-agent-to-rule-them-all-towards-multi-1)

Repository that accompanies [One Agent To Rule Them All: Towards Multi-agent Conversational AI](https://csclarke.com/assets/pdf/ACL_2022.pdf)

### BBAI (Black-Box Agent Integration) Dataset
The dataset collected for this paper is located in the `./data` folder and consists of all question-response pairs used for training the MARS encoder and evaluating the `question agents pairing` and `question response pairing` approaches.

## MARS Encoder for Multi-agent Response Selection
Our [MARS Encoder](https://huggingface.co/csclarke/MARS-Encoder)(Multi-agent Response Selection) model is available for download on HuggingFace [here](https://huggingface.co/csclarke/MARS-Encoder). This model was trained using [SentenceTransformers](https://sbert.net) [Cross-Encoder](https://www.sbert.net/examples/applications/cross-encoder/README.html) class.

### Usage and Performance

MARS Encoder can be used like this:
```python
from sentence_transformers import CrossEncoder
model = CrossEncoder('csclarke/MARS-Encoder')
scores = model.predict([('question 1', 'response 1'), ('question 1', 'response 2')])
```

The model will predict scores for the pairs `('question 1', 'response 1')` and `('question 1', 'response 2')`.

You can use this model also without sentence_transformers and by just using Transformers ``AutoModel`` class

### Reproduce results

Here is a quick script to reproduce the MARS encoder results on `data/test.json`.

```python
import json
import numpy as np
from sentence_transformers import CrossEncoder

label_map = ['alexa', 'google', 'houndify', 'recipe', 'dictionary', 'task_manager', 'hotel', 'stock', 'math', 'sport', 'wikipedia', 'mobile', 'banking', 'coffee', 'event_search', 'jokes', 'reminders', 'adasa', 'covid']

# load MARS encoder
model = CrossEncoder('csclarke/MARS-Encoder')

# load test data
test = json.load(open('data/test.json'))

total = 0
count = 0

# This can be made much faster w/batching
for k, v in test.items():
  responses = [(k,v[label]) for label in label_map]
  scores = model.predict(responses) 
  agent = label_map[np.argmax(scores)]
  
  # Skip examples where no valid agent response is presents
  if "none" in v["human"]:
      continue

  total += 1

  if agent in v["human"]:
      count +=1
print("Accuracy: {}".format(count / total))
```

The baseline models evaluated in this paper can be accessed here:
- [Universal Sentence Encoder](https://tfhub.dev/google/universal-sentence-encoder/4)
- [Universal Sentence Encoder Question Answering (USE QA)](https://tfhub.dev/google/universal-sentence-encoder-qa/2)
- [Roberta+STS](https://huggingface.co/sentence-transformers/stsb-roberta-base)
- [BM25](https://github.com/dorianbrown/rank_bm25)
