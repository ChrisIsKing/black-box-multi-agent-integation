# Data for paper: One Agent to Rule them All: Towards Multi-agent Conversational AI

This dataset is for evaluating the task of Black-box Multi-agent Integration which focuses on combining the capabilities of multiple black-box conversational agents at scale. It provides data to explore two main frameworks of exploration: question agent pairing and question response pairing.

### Dataset statistics

Overall our dataset contains 5550 utterances with 19 question-response pairs per question (one from each of the 19 agents), 105,450 in total across 37 domains. The utterances are split into 3700 utterances (100 examples per domain) for the training set and 1850 (50 per domain) for the test set. The train and test sets respectively contain 2399 and 1186 utterances with at least one positive question-response pair. In the remaining examples, none of the agents were able to achieve annotator agreement (>= 3).

Conversational agents (n=19):
```python
['alexa', 'google', 'houndify', 'recipe', 'dictionary', 'task_manager', 'hotel', 'stock', 'math', 'sport', 'wikipedia', 'mobile', 'banking', 'coffee', 'event_search', 'jokes', 'reminders', 'adasa', 'covid']
```

Domains (n=37): 
```python
['sports', 'hotel', 'wikipedia', 'knowledge', 'recipe', 'jokes', 'covid', 'arithmetic', 'time', 'flight_info', 'weather', 'restaurant_suggestion', 'age', 'geography', 'mobile', 'alarm', 'tip', 'unit_convert', 'translate', 'reminders', 'auto', 'nutrition', 'currency_convert', 'event_search', 'date', 'todo', 'coffee_shop', 'banking', 'calendar', 'dictionary', 'timer', 'travel_suggestion', 'traffic', 'music', 'rand', 'directions', 'stock']
```

Train: 3700 (2399 w/gold response/agent)

Test: 1850 (1186 w/gold response/agent)

Question+Responses pairs: 105,450

### Descriptions.json

This file contains the curated textual descriptions of each of the conversational agents listed. 

### Train & Test.json

This file contains all question response pairs. Each dict object consists of the following:
1. `human_vote`: lists the vote count from crowd workers for each of the agent responses.
2. `intent`: intent of the question.
3. `human`: contains list of agents that achieved > 2 votes.

Here is an example format:
```json
{
    "Show me recipes for salad with tomatoes and croutons and without eggs food": {
        "human_vote": {
            "none": 1,
            "alexa": 1,
            "google": 3,
            "houndify": 0,
            "recipe": 0,
            "dictionary": 0,
            "task_manager": 0,
            "hotel": 0,
            "stock": 0,
            "math": 0,
            "sport": 0,
            "wikipedia": 0,
            "mobile": 0,
            "banking": 1,
            "coffee": 1,
            "event_search": 0,
            "jokes": 0,
            "reminders": 0,
            "adasa": 0,
            "covid": 0,
            "intent": 0
        },
        "alexa": "a recipe from side chef recommends to bake salad in the oven for 15 minutes at 450 degrees Fahrenheit it is recommended to boil tomato for 20 seconds to 30 seconds in boiling water on the stove please tomatoes in boiling water to make them easier to peel quickly place the tomatoes in an ice bath to stop the cooking process a recipe from the kitchen recommends to bake croutons in the oven for 5 minutes at 375 degrees Fahrenheit it is recommended to boil hard-boiled egg for 11 minutes on the stove",
        "google": "okay I've got a recipe called classic panzanella salad Tuscan style tomato and bread salad recipe from Serious Eats this recipe serves 6 and takes about 1 hour to make does that sound good",
        "houndify": "Didn't get that!",
        "recipe": "Sorry, I could not find any matching recipe.",
        "dictionary": "Didn't get that!",
        "task_manager": "Didn't get that!",
        "hotel": "Didn't get that!",
        "stock": "Didn't get that!",
        "math": "Didn't get that!",
        "sport": "Didn't get that!",
        "wikipedia": "Didn't get that!",
        "mobile": "What plan do you want to switch to? I have postpaid and prepaid plans.",
        "banking": "What account do you want the balance for: savings or checking?",
        "coffee": "You've ordered Salad. Correct?",
        "event_search": "For what date/time?",
        "jokes": "Sorry, could you say that again?",
        "reminders": "What was that?",
        "adasa": "Out of scope!",
        "covid": "Speak to our agent on +1 205 512 8171 for more info or you can visit the CDC on https://www.cdc.gov/coronavirus/2019-ncov/index.html or WHO on https://www.who.int/news-room/q-a-detail/q-a-coronaviruses.",
        "intent": "recipe",
        "human": [
            "google"
        ]
    }
 }
```

### Train & Test Classifier.json

This consists of question agent pairs similar to `train.json` but without agent responses. For consists of a 2D array of:
1. The user utterance.
2. List of agents that can correctly resolve utterance.

```json
[
    [
        "Show me recipes for salad with tomatoes and croutons and without eggs food",
        [
            "google"
        ]
    ]
]
```
