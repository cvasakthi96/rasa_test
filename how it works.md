
### All these files are ready for you to use, all you have to do is provide your Google Places API key to credentials.yml file and train the models. Train the NLU model using the command below which will call Rasa NLU train function, pass training data and processing pipeline configuration files, and save the model inside the models/current/nlu_model directory:https://rasa.com/docs/core/0.9.8/tutorial_supervised/

![alt text](rasa_flow.png)

Terminal bot:

here test is project name 
```
step1:


python3.5 -m rasa_nlu.train -c config.yml --data data.json -o models --fixed_model_name nlu_model --project test --verbose

step2:

python3.5 -m rasa_core.train -d domain.yml -s stories.md -o models/jet/dialogue

additional:
-c policy_config.yml

not working with new verstion:
python3.5 -m rasa_core.train  interactive -d domain.yml -s stories.md -o models/test/dialogue  --nlu_threshold 0.2 --core_threshold 0.2 --fallback_action_name 'action_default_fallback'

step3: 

python3.5 -m rasa_core.run  --enable_api -d models/test/dialogue -u models/test/nlu_model --debug --endpoints endpoints.yml

ex:
curl localhost:3000/parse -d '{"q":"hellothere"}'

```


```
fallbaclk:

python -m rasa_core.train -s bot/data/stories -d bot/domain.yml -o bot/models/dialogue --epochs 30 --augmentation 50 --history 3 --nlu_threshold 0.6 --core_threshold 0.6 --fallback_action_name 'utter_default'

```
### custom actions:

```
Run sepratly

python3.5 -m rasa_core_sdk.endpoint --actions actions

```

### view story once after trained iteractively:
```
python3.5  -m rasa_core.visualize -d domain.yml -s stories.md -o graph.html

```

### iteractive training

```
TeacHing our bot interactive ways to train  and building stories using below code:


python3.5 -m rasa_core.train   interactive -o models/jet/dialogue   -d domain.yml -s data/stories.md  --nlu models/jet/nlu_model  --endpoints endpoints.yml

if custom actions included we should use below code for custom actions execution:

python3.5 -m rasa_core_sdk.endpoint --actions actions

```

### once created nlu_model , Run the rasa server to check the nlu_model output using below commands:

```
server start:

python3.5  -m rasa_nlu.server --port 3000 -c config.yaml --path rasa_spacy/models/domain3/

Run in terminal:

curl localhost:3000/parse -d '{"q":"hello there", "project": "project1", "model": "model_20181203-191810"}'

check server status like which project loaded etc...

curl localhost:3000/status
Example:

/home/username/rasa_nlu/projects/domain3/rasa_spacy/models/domain3/model_20181203-184737

python -m rasa_nlu.server  --port 2005 -c config.yaml --pre_load domain2 --path projects/

```
### evaulating entity extractor:

```
python3.5 -m rasa_nlu.evaluate --data invoice.json --model[model folder/modelname]

```
### Reference Link :

(https://github.com/RasaHQ/rasa_core)

(https://github.com/RasaHQ/rasa_core/tree/master/examples/restaurantbot)

(https://github.com/Keerthana786/Pramati/tree/master/Training/Rasa_nlu/My_JetApp)




