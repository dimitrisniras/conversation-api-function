# conversation-service-functions


## what is this project?
this is a cli tool that will allow you to write simple application for the Vonage conversation api https://developer.nexmo.com/conversation in your local env with minimal configuration.







## install prerequisites


### nexmo credentials
To make this app running, you need 
 - a nexmo api key, api secret : https://dashboard.nexmo.com
 - a nexmo phone number (also known as LVN, Long Virtual Number) : https://dashboard.nexmo.com/buy-numbers

### install node 14+
suggested way to install node is via nvm (https://github.com/nvm-sh/nvm/pulls). so: 

#### install nvm
if you have brew install, just run 

```brew install nvm ```

if not, then 
```  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash ```

(read here for more details: https://github.com/nvm-sh/nvm)


### install node with nvm
now that nvm is installed, just run: 

``` nvm install 14 ```


# install the tool

```npm install -g conversation-api-function ```

## first time config

the first time you run this, you need to have your api-key, api-secret and an lvn (look the prerequisites section above):

```conversation-api-function config-new -a <api-key> -s <api-secret> -l <lvn>```

if you struggle with this, run: 
```conversation-api-function config-new -h```

## create a new conversation function

``` conversation-api-function new my_capi_fn ```

## run it

``` conversation-api-function run my_capi_fn ```

now call you lvn, you should hear an "hello world" mesage


open the following file ``` my_capi_fn/index.js ``` for more info

## run it part 2, make your life easier

you can now run every example you find in the `examples` section without the need to configure the app again. 

you can also run the app in an alternative way: 

```
cd my_capi_fn
npm install
npm run
```

in this way you are gonna install the dependencies and run it without the need to use the global tool





## further docs:
check the internal conversations api here: https://jurgob.github.io/conversation-service-docs/#/openapiui
and the possible events here: https://jurgob.github.io/conversation-service-docs/#/custom



## some tricks
This project use a logging library called `bunyan` whitch is producing json logs.
if you install bunyan ( ```npm install -g bunyan ``` ) then you can run: 
`conversation-api-function run my_capi_fn | bunyan`. you will now see a formatted log. 

p.s. bunyan is producing standard json, so you can also use standard unix tools like jq to format the logs: `tail -f vapi_hello_world.log | jq`


## how to write a function

when you start a new project, there's documentation in the example. If you are curious, take.a look here:

https://github.com/jurgob/conversation-api-function/blob/main/template/index.js


## Examples

Once you have configured conversation-api-functions, you can run every project without configuring this tools again. 
Here are some examples you can run just coloning it and executing it with the following commans: 

downloding / installing the repo:
```
git clone <GIT_REPO> <MY_DIR>
cd <MY_DIR>
nvm use
npm install
```
then run it with: 

```  conversation-api-function run <MY_DIR>```


e.g: 
```
git clone https://github.com/jurgob/phone_inbound_asr my_capi_fn
cd my_capi_fn
nvm use
npm install
conversation-api-function run .

```

### Examples 

- **Automatic Speech Recognition**

  git_repo: https://github.com/jurgob/phone_inbound_asr
  
  description: Call a number and trascribe your voice

- **UI react example**

  git_repo: https://github.com/jurgob/react_client_example

  description: a very ugly react interface (genereated using react-create-app) for debuging ip calls. (aka calls from your browser). There's also simple login/subscribe mechanism.

- **NCCO talk action - hello world**

  git_repo: https://github.com/jurgob/capi-fn_ncco_hello_world

  description: NCCO stands for Nexmo Call Control Object. Is an easy way to script your calls

- **NCCO websocket echo repeat**

  git_repo: https://github.com/dimitrisniras/websocket-echo-repeat

  description: Simple Vonage Voice API demo that connects to a websocket endpoint and echoes audio back to caller

  tags: ncco, phone-call, pstn, websocket-call, text-to-speech
  
- **NCCO input of DTMF and Speech**

  git_repo: https://github.com/JohnPeters7116/capi-fn_ncco_dtmf

  description: Simple Vonage Voice API demo that takes dtmf input from customer and sends to customers event url

  tags: ncco, phone-call, pstn, dtmf, speech, text-to-speech

- **Conversations API And facebook messages inbound**

  git_repo: https://github.com/bilalkabat/conversation-messages-inbound-example

  description: Let your customer write a message to your facebook page and store them in conversation api

  tags: conversataion-api, messages-api, facebook-messages, ip-messages,  

- **Conversations API, facebook messages and SMS, both inbound and outbound**
  
  git_repo: https://github.com/andradaioanabogoi/conversation-messages-outbound-example

  description: Store inbound facebook (and whatsapp, viber, sms message) in a conversation. Also respond to them via api (aka outbound messages)

  tags: conversataion-api, messages-api, facebook-messages, ip-messages, whatsapp, facebook messenger, sms, viber

- **Hangup incomming phone calls but send back an SMS**

  git_repo: https://github.com/jurgob/capi-fn-hangup-call-and-send-messages

  description: every phone called received to your LVN are gonna automatically hanged up, but the caller will receive 

  tags: conversataion-api, phone-call, pstn, custom-data, text-to-speech

- **Phone call authenication for IP calls using conversation custom data** 

  git_repo: https://github.com/jurgob/capi-fn-pstn-call-authentication

  description: someone is calling your nexmo number (LVN), he will be asked to say his/her name, The agent on the browser will se the incomming call and the name of the caller.

  tags: conversataion-service, phone call, pstn, custom-data, text-to-speech
  
- **Record a leg or a conversation**

  git_repo (example 1, record by leg): https://github.com/jurgob/capi-fn_record_leg
  
  git_repo (example 2, record by conversation): https://github.com/JohnPeters7116/capi-fn_record_conversation
  
  description: the call in conversations follow the MCU model (https://bloggeek.me/webrtc-multiparty-video-alternatives/).  In a nutshell, there's a mixer (in our case the conversations) where every leg (aka every call partecipant) are mixed togheter. 
If you want to record the call from a leg point of view, that's the example 1 is gonna show how to do it. if you are interested in record all the leg, then check the example 2. 
question: what 's the difference between recording a leg or a converstion?. Immagine leg a is earmuffing leg b. in the leg recording, you will not have the record of the leg b, while in the conversaion record you will have both the legs in the recoring

- **Conversations API And facebook messages with events using Vonage Client JS SDK**

  git_repo: https://github.com/dimitrisniras/inbound-message-chat

  description: Let your customer write a message to your facebook page and store them in conversation api and see all the events that are coming through.

  tags: conversataion-api, messages-api, facebook-messages, ip-messages

- **Inbound PSTN call using Vonage Client JS SDK**

  git_repo: https://github.com/dimitrisniras/inbound-call-example

  description: Perform an inbound PSTN call, calling your nexmo number (LVN) and then connect to an `app` user, transmitting audio and using the JS SDK.

  tags: conversataion-service, phone call, pstn, client sdks

- **Outbound PSTN call using Vonage Client JS SDK**

  git_repo: https://github.com/dimitrisniras/outbound-call-example

  description: Perform an outbound PSTN call to a number, using the JS SDK.

  tags: conversataion-service, phone call, pstn, client sdks

- **Websocket audio phone**

  git_repo:  https://github.com/jurgob/wsphone

  description: receive a phone call and respond using your computer microphone via websocket.

- **Outbound phone call with NCCO**

  git_repo: https://github.com/jurgob/phone_outbound_call_ncco

  description: call a phone number from your application (you could as instance do an automatic phone marketing campaign with this) .

- **Transcribe a conversation**
  
  git_repo (example 1, transcribe by leg): <https://github.com/dimitrisniras/record-leg-transcription>

  git_repo (example 2, transcribe by conversation): <https://github.com/dimitrisniras/record-conversation-transcription>
  
  description: Perform an inbound PSTN call, calling your nexmo number (LVN). The call (or a single leg) will be recorded and transcribed.


## Use a Real Redis

by default the storage client is saving your data in-memory, so every time you restart you loose al your data. 
To use a real redis server instead, you just need to set the env var CONV_API_FUNC_REDIS_URL.
See the example below for more details

### use a docker redis for local deployment

be sure you have installed docker
to install redis in your local host, you just need to run: 
```docker run --name capifn-redis -p 6379:6379 -d redis```


now open your config runnig ```conversation-api-function config```
this is gonna open an editor with your configs. Add this line: 
``` 
CONV_API_FUNC_REDIS_URL="redis://localhost:6379"
```
 



## deploy in production

### create deployment credentials

From the project directory, run the following command: 

```conversation-api-function deploy-new . -a API_KEY -s API_SECRET -l LVN_LIVE```

this is gonna create a `.env.prod` file with the credential to go live

remember, the LVN_LIVE you are using here should be a differnt one then the one you have used in prod. If you use the same, you risk to break your prod application. 

### deploy in heroku. 
After you have create the `.env.prod` file as described above, follow those steps:

1) after you have created a deployment credentials, for the first thing you need to init your project on git: 
```
git init
git add -A
git commit -m 'first commit'

```

2) be sure you have an heroku account:  https://dashboard.heroku.com/apps

3) insatall the heroku cli with ```npm install -g heroku```

4) then you can create an heroku app :

```
heroku login
heroku apps:create my_capi_heroku_app
```

5) now you can finally push the app live.
```
git push heroku main
```

if you look the app logs with ```heroku logs``` you will see that's the app is failing. that's becouse you need to configure the env vars. An easy way is the following: 

```
cat .env.prod | grep -v PRIVATE_KEY | xargs heroku config:set

# set private key
PRIVATE_KEY="`cat .env.prod | grep PRIVATE_KEY | cut -c 27-`"
echo -e $PRIVATE_KEY > private.key
heroku config:set CONV_API_FUNC_PRIVATE_KEY="$PRIVATE_KEY"

# set webhook url
heroku config:set CONV_API_FUNC_SERVER_URL="https://my_capi_heroku_app.herokuapp.com"
```

6) now go to `https://my_capi_heroku_app.herokuapp.com/hello` to check is working












