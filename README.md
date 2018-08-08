# Summary

  | Object | Path |
  | - | - | 
  | [bot](#bot) | `/bot/bots` |
  | [intent](#intent) | `/bot/bots/{bot_id}/intents` |  
  | [entity](#entity) | `/bot/bots/{bot_id}/entities` |  
  | [category](#category) | `/bot/bots/{bot_id}/categories` |  
  | [smart trigger](#smart-trigger) | `/bot/bots/{bot_id}/smarttriggers` |  
  | [Quick Reply](#quick-reply) | `/bot/bots/{bot_id}/quickreplies` |  
  | [learning question](#learning-question) | `/bot/bots/{bot_id}/learningquestions` | 
  | [report](#report) | `/bot/bots/{bot_id}/reports` | 
  | [general](#general) | `/bot/` |

## Bot
  You need `Manage Bot` permission to manage bot and customize the settings for a bot.
  - `Bots` - Bot Manage
    + `GET /api/v1/bot/bots` - [Get all bots of a site](#get-all-bots-of-a-site)
    + `POST /api/v1/bot/bots` - [Create a new bot](#create-a-new-bot)
    + `PUT /api/v1/bot/bots/{id}` - [Update a bot](#update-a-bot)
    + `GET /api/v1/bot/bots/{id}` - [Get a bot by id](#get-a-bot-by-id)
    + `DELETE /api/v1/bot/bots/{id}` - [Remove a bot](#remove-a-bot)
    + `POST /api/v1/bot/bots/{id}/export` - [Export a bot](#export-a-bot)
    + `POST /api/v1/bot/bots/{id}/import` - [Import a bot](#import-a-bot)
    + `POST /api/v1/bot/bots/{id}/train` - [Train a bot](#train-a-bot)
    + `GET /api/v1/bot/bots/{id}/availability`  - [Check if the bot is available](#check-if-the-bot-is-available)
    + `POST /api/v1/bot/bots/{id}/test`  - [Test a bot](#test-a-bot)
    + `POST /api/v1/bot/bots/{id}/sendMessage` - [Callback for webview, send message to visitor](#callback-for-webview,-send-message-to-visitor)
    + `POST /api/v1/bot/bots/{id}/queryIntent` - [chat with bot](#chat-with-bot)

### Bot Related Object Json Format

#### QueryIntentParameter

  QueryIntentParameter is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `channelType` | string  | no | yes | type of the channel,including `liveChat`、`faceBook` and `twitter` |
  | `operationType` | string  | no | yes | type of the operation,including `queryIntent`、`goToIntent`、`viaForm`、`signedIn`、`requestLocation` and `viaPrompts` |
  | `formValues` | [FormValues](#formValue) | no | no | an array of form value |
  | `sessionId` | string  | no | yes | sessionId of the chat |
  | `isHelpful` | boolean  | no | no | whether bot answer is helpful,`true` or `false` |
  | `question` | string  | no | yes | question of the chat |
  | `intentId` | integer  | no | yes | intentId of the bot |
  | `chatId` | integer  | no | yes | chatId of the chat |
  | `senderId` | integer  | no | no | senderId of the chat |
  | `senderType` | integer  | no | no | senderId of the chat |
  | `questionId` | string  | no | yes | questionId of the bot |
  | `campaignId` | integer  | no | yes | id of the campaign setting |
  | `visitorInfo` | [VisitorInfo](#visitorInfo)  | no | yes | visitor info object |

#### FormValue

  Form Value is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `lable` | string  | no | yes | lable of the formValue |
  | `value` | string  | no | yes | value of the formValue |

#### VisitorInfo

  Visitor info is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer | yes | no | id of the visitor |
  | `longitude` | float | no | no | longitude of the visitor location |
  | `latitude` | float | no | no | latitude of the visitor location |
  | `page_views` | integer | no | yes | count of the visited |
  | `browser` | string | no | yes | visitor use browser type |
  | `chats` | integer | no | yes | count of chat |
  | `city` | string | no | yes | the city of the visitor |
  | `company` | string | no | yes | the company of the visitor |
  | `country` | string | no | yes | the country of the visitor |
  | `current_browsing` | string | no | yes | page of the current browsing |
  | `custom_fields` | [CustomFields](#customfields) | no | yes | an array of custom fields |
  | `custom_variables` | [CustomVariables](#customvariables) | no | yes | an array of custom variables |
  | `department` | string | no | yes | department of the visitor |
  | `email` | string | no | yes | email of the visitor |
  | `first_visit_time` | string | no | yes | the time of first visit |
  | `flash_version` | string | no | yes | version of the flash |
  | `ip` | string | no | yes | ip of the visitor |
  | `keywords` | string | no | yes | search engine key |
  | `landing_page` | string | no | yes | the page of login |
  | `language` | string | no | yes | language |
  | `name` | string | no | yes | name of the visitor |
  | `operating_system` | string | no | yes | operating system of the visitor |
  | `phone` | string | no | yes | phone of the visitor |
  | `product_service` | string | no | yes | product service |
  | `referrer_url` | string | no | yes | referrer url |
  | `screen_resolution` | string | no | yes | screen resolution |
  | `search_engine` | string | no | yes | search engine |
  | `state` | string | no | yes | state of the visitor |
  | `status` | string | no | yes | status of the visitor |
  | `time_zone` | string | no | yes | time zone of the visitor |
  | `visit_time` | string | no | yes | time of the visitor |
  | `visits` | integer | no | yes | count of the visited |
  | `ssoId` | string | no | no | sso id |

#### CustomFields

  Custom fields is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the field |
  | `name` | string  | no | yes | name of the field |
  | `value` | string  | no | yes | value of the field |

#### CustomVariables

  Custom variables is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `name` | string  | no | yes | name of the variable |
  | `value` | string  | no | yes | value of the variable |

#### QueryIntentResponse

  QueryIntentResponse is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `type` | string  | no | yes | type of the response,including `signIn`、`viaForm`、`viaPrompts`、`highConfidenceAnswer`、`possibleAnswer`、`noAnswer` and `requestLocation` |
  | `chatId` | integer  | no | yes | chatId of the chat |
  | `question` | string | no | no | question of the chat |
  | `siteId` | integer  | no | yes | siteId of the bot |
  | `visitorId` | integer  | no | yes | id of the visitor |
  | `senderType` | string  | no | yes | type of the sender,including `agent` and `bot` |
  | `intentId` | integer  | no | yes | id of the intent |
  | `questionId` | string  | no | yes | id of the intent question |
  | `ifRate` | boolean  | no | yes | rate chat,`true` or `false` |
  | `content` | object | no | yes | response's content. when type is signIn, it represents [SignInResponse](#signinresponse);when type is viaForm or viaPrompts ,it represents [EntityCollectionResponse](#entitycollectionresponse);when type is highConfidenceAnswer, it represents [HighConfidenceResponse](#highconfidenceresponse); when type is possibleAnswer,it represents [PossibleResponse](#possibleresponse);when type is noAnswerResponse,it represents [NoAnswerResponse](#noanswerresponse);when type is requestLocationResponse, it represents [RequestLocationResponse](#requestlocationresponse). |

#### HighConfidenceResponse

  High confidence response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `smartTriggerActions` | [SmartTriggerAction](#actionex)  | no | yes | an array of smart trigger actions |
  | `intentAnswers` | [Response](#response-object)  | no | yes | an array of intent answers |

#### SignInResponse

  Sign in response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `signInMessage` | string  | no | yes | message of the sign in |
  | `signInLinkText` | string  | no | yes | text of the sign in link |
  | `isSSO` | boolean  | no | yes | is sso,`true` or `false` |
  | `signInURL` | string  | no | yes | url of the sign in |
  | `customVariable` | string  | no | yes | custom variable |
  | `openIn` | string  | no | yes | it is a Enum string. with options `sideWindow`, `newWindow`, `currentWindow` |
  | `smartTriggerActions` | [SmartTriggerAction](#actionex)  | no | yes | an array of smart trigger actions |

#### EntityCollectionResponse

  Entity collection response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `viaPrompts` | [ViaPrompts](#viaprompts)  | no | yes | an array of via prompts |
  | `viaForm` | [ViaForm](#viaform)  | no | yes | an via form object |
  | `smartTriggerActions` | [SmartTriggerAction](#actionex)  | no | yes | an array of smart trigger actions |

#### ViaPrompts

  Via prompts is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `prompt` | string  | no | yes | text of the prompt |
  | `options` | array  | no | yes | an array of string quick reply |
 
#### ViaForm

  Via form is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `formMessage` | string  | no | yes | name of the field |
  | `formTitle` | string  | no | yes | name of the field |
  | `submitButtonText` | string  | no | yes | submit button text |
  | `cancelButtonText` | string  | no | yes | cancel button text |
  | `confirmButtonText` | string  | no | yes | confirm button text |
  | `fields` | [Fields](#fields)  | no | yes | an array of fields |

#### Fields

  Fields is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `value` | string  | no | yes | name of the field |
  | `name` | string  | no | yes | title of the field |
  | `type` | string  | no | yes | type of the field,including `text`、`textArea`、`radio`、`checkBox`、`dropDownList`、`checkBoxList`、`attachment`、`rating`、`wrapUpCategory` and `wrapUpComment` |
  | `isRequired` | boolean  | no | yes | is require, `true` or `false` |
  | `isMasked` | boolean  | no | yes | is mask,`true` or `false` |
  | `options` | array  | no | yes | an array of string entity collecion prompts |

#### PossibleResponse

  Possible response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `possibleResponsesMessage` | string  | no | yes | message of the possible responses |
  | `intentBase.id` | int  | no | yes | an array of intents  |
  | `intentBase.name` | string  | no | yes | an array of intents  |
  | `smartTriggerActions` | [SmartTriggerAction](#smarttriggeraction)  | no | yes | an array of smart trigger actions |

#### NoAnswerResponse

  No answer response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `noResponseMessage` | string  | no | yes | message of the no response |
  | `noResponseTextWhenAgentIsOnline` | string  | no | yes | text of the no response when agent is on line |
  | `noResponseTextWhenAgentIsOffline` | string  | no | yes | text of the no response when agent is off line |
  | `smartTriggerActions` | [SmartTriggerAction](#smarttriggeraction)  | no | yes | an array of smart trigger actions |

#### RequestLocationResponse

  Request location response is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `requestVisitorLocationMessege` | string  | no | yes | message of the request visitor location |
  | `askVisitorShareLocationText` | string  | no | yes | text of the ask visitor share location |
  | `url` | string  | no | yes | url |
  | `smartTriggerActions` | [SmartTriggerAction](#actionex)  | no | yes | an array of smart trigger actions |

#### TestBotResponse

  TestBotResponse is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `intentId` | integer  | no | yes | id of the intent |
  | `intentName` | string  | no | yes | name of the intent |
  | `score` | float  | no | yes | score of match intent |
  | `noAnswerScore` | float  | no | yes | no answer score of the settings |
  | `type` | string  | no | yes | type of the response,including `form`、`signIn`、`response` and `location` and `prompts` |
  | `answer` | object  | no | yes | type of the answer,including [ViaPrompts](#viaprompts)、[ViaForm](#viaForm) 、list of [Response](#response-object)、[SignInResponse](#signinresponse) and [RequestLocationResponse](#requestlocationresponse) |

#### RateParameter

  RateParameter is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `isHelpful` | boolean  | no | yes | whether bot answer is helpful,`true` or `false` |
  | `questionId` | string  | no | yes | questionId of the bot |
  | `chatId` | integer  | no | yes | chatId of the chat |
  | `visitorInfo` | [VisitorInfo](#visitorinfo)  | no | yes | visitor info object |

#### RateResponse

  RateParameter is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `result` | string  | no | yes | message of the rate |
  | `smartTriggerActions` | [SmartTriggerAction](#smarttriggeraction)  | no | yes | an array of smart trigger actions |

#### CreateBot
  CreateBot is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `name` | string  | no | yes | name of the bot |
  | `language` | string  | no | yes | language of the bot |

#### BotBasic
  Bot is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the bot |
  | `name` | string  | no | yes | name of the bot |
  | `language` | string  | no | yes | language of the bot |  
  | `avatarName` | string  | no | yes | avatar name of the bot |  
  | `avatarUrl` | string  | no | yes | avatar url of the bot |  
  | `isTrained` | bool  | no | yes | if the bot is trained |  

#### Bot Object
  Bot is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the bot |
  | `name` | string  | no | yes | name of the bot |
  | `language` | string  | no | yes | language of the bot |  
  | `avatarName` | string  | no | yes | avatar name of the bot |  
  | `avatarUrl` | string  | no | yes | avatar url of the bot |  
  | `isTrained` | bool  | no | yes | if the bot is trained |  
  | `greetingMessage` | object  | no | yes | list of [GreetingMessage](#greetingmessage) Object | 
  | `noResponseMessage` | string  | no | yes | no response message |  
  | `isShowAgentLinkWhenNoResponse` | bool  | no | yes | is show agent link when no response from bot |  
  | `notHelpfulMessage` | string  | no | yes | not helpful message |  
  | `isShowAgentLinkWhenNotHelpful` | bool  | no | yes | is show agent link when not helpful from bot |  
  | `possibleResponsesMessage` | string  | no | yes | possible responses message |  
  | `possibleResponsesThreshold` | int  | no | yes | possible responses threshold |  
  | `isShowAgentLinkWhenPossibleResponsesThreshold` | int  | no | yes | is show agent link when possible responses threshold |  
  | `possibleResponsesExceedThresholdMessage` | string  | no | yes | possible responses exceed threshold message |  
  | `agentIsOnlineText` | string  | no | yes | agent is online text |  
  | `agentIsOfflineText` | string  | no | yes | agent is offline text |  
  | `transferAgentMessege` | string  | no | yes | transfer agent messege |  
  | `leaveAMessageClickedMessege` | string  | no | yes | leave a message button clicked messege |  
  | `requestVisitorLocationMessege` | string  | no | yes | request visitor location messege |  
  | `locationButtonText` | string  | no | yes | location button text |  
  | `submitButtonText` | string  | no | yes | submit button text |  
  | `cancelButtonText` | string  | no | yes | cancel button text |  
  | `confirmButtonText` | string  | no | yes | confirm button text |  
  | `highConfidenceScore` | string  | no | yes | high confidence score |  
  | `noAnswerScore` | string  | no | yes | no answer score |  
 
#### Campaign
  Campaign is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Campaign |
  | `name` | string  | no | yes | name of the Campaign |
  | `url` | string  | no | yes | url of the Campaign |  

#### NameUrl
  NameUrl is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `name` | string  | no | yes | name of the object |
  | `url` | string  | no | yes | url of the object |  

#### SendMessageParameter

  SendMessageParameter is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `channelType` | string  | no | yes |enums contain default,livechat,facebook and twitter.|
  | `agentId` | integer  | no | yes | agentId of the chat |
  | `sessionId` | integer  | no | yes | sessionId of the chat |
  | `visitorId` | integer  | no | yes | visitorId of the chat |
  | `messages` | list of [Response](#response-object)  | no | yes | an array of responses  |

### Bot End Points
#### Get all bots of a site

  `GET /api/v1/bot/bots`

##### Parameters

query parameters

  - `siteId ` 

##### Response
the response is: list of [BotBasic](#botbasic) Objects

#### create a new bot

  `POST /api/v1/bot/bots`

##### Parameters
query parameters

  - `siteId ` 

request body parameters: [CreateBot](#createbot) Object

##### Response
the response :  [BotBasic](#botbasic) Object

#### Update a bot

  `PUT /api/v1/bot/bots/{id}`

##### Parameters
path parameters

  - `id`

request body parameters: [Bot](#bot-object) Object

##### Response
the response is: [Bot](#bot-object) Object

#### Get a bot by id

  `GET /api/v1/bot/bots/{id}`

##### Parameters
path parameters

  - `id`

##### Response
When the Http Status Code is 200, the response is: [Bot](#bot-object) Objects

#### Remove a bot

  `DELETE /api/v1/bot/bots/{id}`

##### Parameters
path parameters

  - `id`

##### Response
the response is: Http Status Code `200`

#### Export a bot

  `POST /api/v1/bot/bots/{id}/export`

##### Parameters
path parameters

  - `id`

##### Response
the response is:

  - `fileName ` -the exported bot fileName, it is a xml file

#### Import a bot

  `POST /api/v1/bot/bots/{id}/import`

##### Parameters
path parameters

  - `id`

query parameters

  - `file` -the file to be imported. Server will get the file by Request.files["file"]

##### Response
the response is:

when the status is `Processing `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `operationId ` - it is a guid, uniquely identify the import operation

when the status is `Failed `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `errorMessage ` 

when the status is `Succeeded `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `

#### Train a bot

  `POST /api/v1/bot/bots/{id}/train`

##### Parameters
path parameters
  
  - `id`

##### Response
the response is:

  - `operationId ` -the operation id of the train

#### Check if the bot is available

  `GET /api/v1/bot/bots/{id}/availability`

##### Parameters
  path parameters

  - `id`

##### Response
the response is:

  - `isAvailable ` -true or false

#### Test a bot

  `POST /api/v1/bot/bots/{id}/test`

##### Parameters
path parameters

  - `id`

request body parameters

  - `question`  - test visitor question

##### Response
the response is: [TestBotResponse](#testbotresponse) Object 

#### Callback for webview, send message to visitor

  `POST /api/v1/bot/bots/{id}/sendMessage`

##### Parameters
path parameters

  - `id`

query parameters

  - `siteId`

request body parameters: [SendMessageParameter](#sendmessageparameter) Object 

##### Response
the response is: Http Status Code `200`

#### Chat with bot

  `POST /api/v1/bot/bots/{id}/queryIntent`

##### Parameters
path parameters

  - `id`-id of the bot

request body parameters: [QueryIntentParameter](#queryintentparameter) Object 

##### Response
the response is: [QueryIntentResponse](#queryintentresponse) Object             

## Intent
You need `Manage Bot` permission to manage Intent and customize the settings for a Intent.
  - `Intents` - Intent Manage
  +  `POST /api/v1/bot/bots/{botId}/intents` - [Create a new intent](#create-a-new-intent)
  +  `GET /api/v1/bot/bots/{botId}/intents` - [Get intent(s) by category or by intent name/question](#get-intent(s)-by-category-or-by-intent-namequestion)
  +  `PUT /api/v1/bot/bots/{botId}/intents/{id}` - [Update a intent](#update-a-intent)
  +  `GET /api/v1/bot/bots/{botId}/intents/{id}` - [Get an intent](#get-an-intent)
  +  `DELETE /api/v1/bot/bots/{botId}/intents/{id}` - [Remove an intent](#remove-an-intent)
  +  `POST /api/v1/bot/bots/{botId}/intents/{id}/rating` - [Rate a bot answer as helpful or not helpful](#rate-a-bot-answer-as-helpful-or-not-helpful)
  +  `POST /api/v1/bot/bots/{botId}/intents/import` - [Import intents](#import-intents)

### Intent Related Ojbect Json Format
#### Intent Object
Intent is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description   |
| - | - | :-: | :-: | - | 
| `id` | integer  | yes | no | id of the intent |
| `name` | string  | no | yes | name of the intent |
|`categoryId`| integer | no | yes | id of the intent category.|
|`ifRequireDetailInfo` | bool | no | no | whether need visitor to provide more detail information.|
|`entityCollectionType` | string | no | yes if ifRequireDetailInfo is true | enums contain viaForm and viaPrompts,this represents the way you want to collect  visitor's information. there are two options: viaForm and viaPrompts.|
|`ifRequireLocation` | bool | no | yes | whether need to collect visitor's location information.|
|`questions`| array| no |yes | an array of [Question](#question).|
|`entityCollectionForm`| object | no |yes if entityCollectionType is viaForm | an array of [EntityCollectionForm](#entitycollectionform).|
|`entityCollectionPrompts`| array| no |yes if entityCollectionType is viaPrompts | an array of [EntityCollectionPrompt](#entitycollectionprompt).|
|`answer`| object| no |yes | an item of [Answer](#answer).|

#### IntentBasic
IntentBasic is represented as simple flat json objects with the following keys: 

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
| `id` | integer  | yes | no | id of the intent |
| `name` | string  | no | yes | name of the intent |
|`category`| string | no | yes | name of the intent category.|
|`categoryId`| integer | no | yes | id of the intent category.|

#### AnswerSignInSettings
AnswerSignInSettings is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item.|
|`signInMessage` | string  | no | yes |text sent to visitor before signin in button.|
|`signInLinkText` | string  | no | yes |text on signin button.|
|`isSSO` | string  | no | yes |whether is single sign on.|
|`signInURL` | string  | no | yes |url of the signin page.|
|`customVariable` | string  | no | yes |custom value sent to signin page.|
|`openIn` | string  | no | yes |enums contain sideWindow,newWindow,currentWindow,when channelType is livechat, it represents the way that a page will be opened.|

#### Question
Question is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item.|
|`text` | string  | no | yes |question you can expect from users,that will trigger this intent. |
|`entityLabels` | array  | no | yes |an array of [EntityLabel](#entitylabel) that you want to mark on current question. |

#### EntityLabel
EntityLabel is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item. |
|`startPos` | integer | no | yes |strat index  of current question you marked. |
|`endPos` | integer | no | yes |end index  of current question you marked. |
|`entityId` | integer | no | yes |id of entity marked on one question. |
|`label` | string | no | yes |label to distinguish same entity marked on one question. |

#### EntityCollectionForm
EntityCollectionForm is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`formMessage` | string | no | yes if entityCollectionType is viaForm | when entityCollectionType is viaForm, this is a message that will be sent before the button.|
|`formTitle` | string | no | yes if entityCollectionType is viaForm | when entityCollectionType is viaForm,a button will be sent to visitor if bot need to collect detail information,visitor can click this button to open the form to fillout information. this is the text on this button,and also this is the title of that form.|
|`ifRequireConfirm` | bool | no | yes | whether need visitor to confirm after collect all detail information that bot needed.|
|`formFields` | array | no | no |an array of of [EntityCollectionFormField](#entitycollectionformfield) |

#### EntityCollectionFormField
EntityCollectionFormField is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item. |
|`fieldType` | string | no | yes |enums contain text ,textArea,radioBox ,checkBox ,dropDownList ,checkBoxList, this is the type of fields appear on the form. |
|`fieldName` | string | no | yes |this is the field's name appear on the form. |
|`entityId` | integer | no | yes |id of entity marked on one question. |
|`label` | string | no | yes |label to distinguish same entity marked on one question. |
|`isRequired` | bool | no | yes |it marks whether the field appear on the form is required or not. |
|`isMasked` | bool | no | yes |if this is true,visitor's information will replaced by anonymous symbol in chat logs. |
|`options` | array | no | no |an array of of string |

#### EntityCollectionPrompt
EntityCollectionPrompt is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    | Mandatory | Description  |  
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item. |
|`entityId` | integer | no | yes |id of entity marked on one question. |
|`label` | string | no | yes |label to distinguish same entity marked on one question. |
|`questions` | array | no | yes |an array of string |
|`options` | array | no | no |an array of string |

#### TextResponse
TextResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description  |  
| - | - | :-: | :-: | - | 
|`texts` | array | no | yes |an array of list strings. |

#### UrlResponse
UrlResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`url` | string | no | yes |url of the video you choosed.  | 

#### ComplexResponse
ComplexResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`text` | string | no | yes |html text updated from old data.  | 

#### QuickReplyResponse
QuickReplyResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`text` | string | no | yes |text sent before quickreplys.  | 
|`quickReplyId` | integer | no | yes |id of quickreply you choosed.  | 

#### ButtonResponse
ButtonResponse is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description   |   
| - | - | :-: | :-: | - | 
|`text` | string | no | yes |text above buttons,this text will be sent before buttons.  | 
|`buttons` | array | no | yes |an array of [Button](#button).  | 

#### Button
Button is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item.  | 
|`text` | string | no | yes |text on button.  | 
|`type` | string | no | yes |enums contain goToIntent,link and webView,type of buttons  | 
|`linkUrl` | string | no | yes if buttonType is link or webView|url of the web page you want to open.  | 
|`intentId` | string | no | yes if buttonType is goToIntent | id of the intent you choosed.  | 
|`intentName` | string | no | yes if buttonType is goToIntent | the name of the intent you choosed.  | 
|`openIn` | string | no | yes if channelType is livechat and buttonType is link or webView |enums contain sideWindow,newWindow,currentWindow, it represents the way that a page will be opened.  | 
|`openStyle` | string | no | yes if channelType is livechat or facebook and buttonType is webView |enums contain compact,tall and full,it represents the size of the webview that will be opened.  |

#### Answer
Answer is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`default`| object| no |no | an object of [AnswerSubItem](#answersubitem),but AnswerSubItem.response.type can not be image,video,webhook,complex.  | 
|`livechat`| object| no |no | an object of [AnswerSubItem](#answersubitem).  | 
|`facebook`| object| no |no | an object of [AnswerSubItem](#answersubitem),but AnswerSubItem.response.type can not be complex.  | 
|`twitter`| object| no |no | an object of [AnswerSubItem](#answersubitem),but AnswerSubItem.response.type can not be complex.  | 

#### GreetingMessage
GreetingMessage is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`default`| list of object | no |no | list of [Response](#response-object),but response.type can not be image,video,webhook,complex.  | 
|`livechat`| list of object | no |no | list of [Response](#response-object).  | 
|`facebook`| list of object | no |no | list of [Response](#response-object),but response.type can not be complex.  | 
|`twitter`| list of object | no |no | list of [Response](#response-object),but response.type can not be complex.  | 

#### AnswerSubItem
AnswerSubItem is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`responses`| list of object | no |no | an array of [Response](#response-object)  | 
|`ifNeedSignIn`| bool | no |yes | whether need sign in when bot response visitor's question     | 
|`signInSettings`| object | no |yes if isNeedSignInBeforeBotRespond is true | an item of [AnswerSignInSettings](#answersigninsettings)  | 

#### Response Object
Response is represented as simple flat json objects with the following keys:

|Name| Type| Read-only    |Mandatory | Description     | 
| - | - | :-: | :-: | - | 
|`id` | integer  | yes | no |id of the current item.  | 
|`type` | string | no | yes |enums contain text,image,video,webhook,button,quickReply,complex.  | 
|`content` | object | no | yes |response's content. when type is text, it represents [TextResponse](#textresponse);when type is image ,it represents [ImageResponse](#nameurl);when type is video, it represents [VideoResponse](#urlresponse); when type is webhook,it represents [WebhookResponse](#urlresponse);when type is button,it represents [ButtonResponse](#buttonresponse);when type is quickReply, it represents [QuickReplyResponse](#quickreplyresponse);when type is complex,it represents   [ComplexResponse](#complexresponse).  | 

#### Create a new intent

  `POST /api/v1/bot/bots/{botId}/intents`

##### Parameters
  path parameters

  - `botId` - required , id of current bot

  query parameters

  - `learningQuestionId` - int,id from visitor's  not matched  questions,optional

  request body parameters

  - `intent` - an item of [Intent](#intent-object),required

##### Response
the response is:

  - `intent` - an item of [Intent](#intent-object),required

#### Update a intent

  `PUT /api/v1/bot/bots/{botId}/intents/{id}`

##### Parameters
  path parameters

  - `id`
  - `botId` - required , id of current bot
  query parameters

  - `learningQuestionId` - int,id from visitor's  not matched  questions,optional

  request body parameter

  - `intent` - an item of [Intent](#intent-object),required

##### Response
the response is:

  - `intent` - an item of [Intent](#intent-object)

#### Get intent(s) by category or by intent name/question

  `GET /api/v1/bot/bots/{botId}/intents`

##### Parameters

  path parameters
  - `botId` - id of current bot,required

  query parameters

  - `categoryId` -id of the category you want to explorer
  - `keyword` -name or question of the intent you want to explorer

##### Response
the response is:

  - `intentBasics` - an array of [IntentBasic](#intentbasic)

####  Get an intent

   `GET /api/v1/bot/bots/{botId}/intents/{id}`

##### Parameter

  path parameters
  - `botId` - id of current bot,required
  - `id` - id of the intent you want to get,required

##### Response
the response is:

  - `intent` - an item of [Intent](#intent-object)

#### Remove an intent

  `DELETE /api/v1/bot/bots/{botId}/intents/{id}`

##### Parameter
path parameters

- `botId `
- `id`

##### Response
the response is: Http Status Code `200`

#### Rate a bot answer as helpful or not helpful

  `POST /api/v1/bot/bots/{botId}/intents/{id}/rating`

##### Parameters
path parameters

  - `botId`-id of the bot
  - `id`-id of the intent

request body parameters: [RateParameter](#rateparameter) Object 

##### Response
the response is: [RateResponse](#rateresponse) Object 

#### Import intents

  `POST /api/v1/bot/bots/{botId}/intents/import`

##### Parameters
path parameters

  - `botId` 
  - `mode` - enum values, `increment` or `overwrite`
 
query parameters

  - `file` -the file to be imported. Server will get the file by Request.files["file"]

##### Response
the response is:

when the status is `Processing `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `operationId ` - it is a guid, uniquely identify the import operation

when the status is `Failed `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `failUrl ` 
  - `errorMessage ` 

when the status is `Succeeded `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `

## Entity
  You need `Manage Bot` permission to manage bot Entity and customize the settings for a bot Entity.
  - `Entities` - Entity Manage
    + `GET /api/v1/bot/bots/{botId}/entities` - [Get entities by entity name/keyword/synonym](#get-entities-by-entity-name/keyword/synonym)
    + `POST /api/v1/bot/bots/{botId}/entities` - [Create a new entity](#create-a-new-entity)
    + `PUT /api/v1/bot/bots/{botId}/entities/{id}` - [Update an entity](#update-an-entity)
    + `DELETE /api/v1/bot/bots/{botId}/entities/{id}` - [Remove an entity](#remove-an-entity)
    + `GET /api/v1/bot/bots/{botId}/entities/{id}` - [Get an entity by id](#get-an-entity-by-id)
    + `POST /api/v1/bot/bots/{botId}/entities/import` - [Import entities](#import-entities)

### Entity Related Objects Json Format
#### EntityBasic
  EntityBasic is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Entity |
  | `name` | string  | no | yes | name of the Entity |
  | `displayName` | string  | no | yes | display name of the Entity |
  | `type` | string  | no | yes | type of the Entity, it is a enum value. `entity` or `systemEntity` |

#### Entity Object
  Entity is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Entity |
  | `name` | string  | no | yes | name of the Entity |
  | `displayName` | string  | no | yes | display name of the Entity |
  | `type` | string  | no | yes | type of the Entity, it is a enum value. `entity` or `systemEntity` |
  | `keywords` | list of [EntityKeyword](#entitykeyword) Objects   | no | yes | keyword and the synonyms list of the keyword |

#### EntityKeyword
 EntityKeyword is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Entity |
  | `keyword` | string  | no | yes | name of the Entity |
  | `synonyms` | list of string  | no | yes | synonyms list of keyword |


### Entity End Points
#### Get entities by entity name/keyword/synonym

  `GET /api/v1/bot/bots/{botId}/entities`

##### Parameters
path parameters

  - `botId` 
  
query parameters

  - `keyword ` -entity name or keyword or synonym

##### Response
the response is: list of [EntityBasic](#entitybasic) Objects
  
#### Create a new entity

  `POST /api/v1/bot/bots/{botId}/entities`

##### Parameters
path parameters

  - `botId` 

request body parameters: [Entity](#entity-object) Object

##### Response
the response is: [Entity](#entity-object) Object

#### Update an entity

  `PUT /api/v1/bot/bots/{botId}/entities/{id}`

##### Parameters
path parameters

  - `id`
  - `botId` 

request body parameters: [Entity](#entity-object) Object

##### Response
the response is: [Entity](#entity-object) Object

#### Remove an entity

  `DELETE /api/v1/bot/bots/{botId}/entities/{id}`

##### Parameters
path parameters

  - `botId `
  - `id ` 

##### Response
the response is: Http Status Code `200`

#### Get an entity by id

  `GET /api/v1/bot/bots/{botId}/entities/{id}`

##### Parameters
path parameters

  - `botId` 
  - `id `

##### Response
the response is: [Entity](#entity-object) Object

#### Import entities

  `POST /api/v1/bot/bots/{botId}/entities/import`

##### Parameters
path parameters

  - `botId` 

query parameters

  - `file` -the file to be imported. Server will get the file by Request.files["file"]

##### Response
the response is:

when the status is `Processing `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `operationId ` - it is a guid, uniquely identify the import operation

when the status is `Failed `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `failUrl ` 
  - `errorMessage ` 

when the status is `Succeeded `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `

## Category
  You need `Manage Bot` permission to manage bot category and customize the settings for a bot category.
  - `Categories` - Category Manage
    + `GET /api/v1/bot/bots/{botId}/categories` - [Get all categories of the bot](#get-all-categories-of-the-bot)
    + `POST /api/v1/bot/bots/{botId}/categories` - [Create a new category](#create-a-by-new-category)
    + `PUT /api/v1/bot/bots/{botId}/categories/{id}` - [Update a category](#update-a-category)
    + `DELETE /api/v1/bot/bots/{botId}/categories/{id}` - [Remove a category](#remove-a-category)

### Category Related Object Json Format
#### Category
  Category is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Category |
  | `name` | string  | no | yes | name of the Category |
  | `parentId` | integer  | no | yes | parent Id of the Category |
  | `botId` | integer  | no | yes | bot id of the Category |

### Category End Points
#### Get all categories of the bot

  `GET /api/v1/bot/bots/{botId}/categories`

##### Parameters
path parameters

  - `botId` 

##### Response
the response is: list of [Category](#category) Objects

#### Create a new category

  `POST /api/v1/bot/bots/{botId}/categories`

#####  Parameters
path parameters

  - `botId` 

request body parameters: [Category](#category) Object

##### Response
the response is: [Category](#category) Object

#### Update a category

  `PUT /api/v1/bot/bots/{botId}/categories/{id}`

##### Parameters
path parameters

  - `id`
  - `botId` 

request body parameters: [Category](#category) Object

##### Response
the response is: [Category](#category) Object

#### Remove a category

  `DELETE /api/v1/bot/bots/{botId}/categories/{id}`

##### Parameters
path parameters

  - `botId` 
  - `id ` 

##### Response
the response is: Http Status Code `200`

## Smart Trigger
  You need `Manage Bot` permission to manage Smart Triggers.
  - `Smart Triggers` - Smart Trigger Manage
    + `POST /api/v1/bot/bots/{botId}/smartTriggers` -[Create a new smart trigger](#create-a-new-smart-trigger)
    + `GET /api/v1/bot/bots/{botId}/smartTriggers` -[Get all smart triggers of the bot](#get-all-smart-triggers-of-the-bot)
    + `GET /api/v1/bot/bots/{botId}/smartTriggers/{id}`  -[Get a smart trigger by id](#get-a-smart-trigger-by-id)
    + `PUT /api/v1/bot/bots/{botId}/smartTriggers/{id}`  -[Update a smart trigger](#update-a-smart-trigger)
    + `DELETE /api/v1/bot/bots/{botId}/smartTriggers/{id}`  -[Remove a smart trigger](#remove-a-smart-trigger)
    + `PUT /api/v1/bot/bots/{botId}/smartTriggers/order`  -[Update the order of smart triggers](#update-the-order-of-smart-trigger-)

### Smart Trigger Related Ojbect Json Format
#### TriggerRule

  TriggerRule is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | yes | no |id of the smart trigger. |
  | `name` | string | no | yes |name of smart trigger. |
  | `isEnabled` | boolean | no | no |smartTriggers if is enabled. the default value is false.|
  | `conditions` | [Conditions](#conditions) | no | no |[Conditions](#conditions) object. |
  | `actions` | array | no | no |an array of [Action](#action) object. |

####  Conditions
  Conditions is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `when` | string | no | yes | the relationship between condition.  exp: [all,or,expression]|
  | `expression` | string | no | no |A formula to calculate exp:(1 or 2) and 3  |
  | `items` | array | no | no | an array of  [Condition](#condition) object. |

 #### Condition
  Condition is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `variable` | string | no | no | value of the Condition |
  | `expression` | string | no | yes |  the rule of expression.exp:[equal,notEqual,contains,notContains,regularExpression,lessThan,moreThan] |
  | `values` | array | no | yes | an string array of condition matching value |
 
####  Action
  Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `type` | string | no | yes | the type of the action. exp:[notifications,monitor,transfer,changeAssignee,segment]|
  | `isEnabled` | boolean | no | yes | action if is enabled. |
  | `target` | [Target](#target) | no | no |  action target |
  | `agentOfflineMessage` | string | no | no | agent offlineMessage prompt message |

####  ActionEx
  Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `Action.type` | string | no | yes | the type of the action. exp:[notifications,monitor,transfer,changeAssignee,segment]|
  | `Action.isEnabled` | boolean | no | yes | action if is enabled. |
  | `Action.target` | [Target](#target) | no | no |  action target |
  | `Action.agentOfflineMessage` | string | no | no | agent offlineMessage prompt message |
  | `agentOfflineText` | string | no | no | leave message button text when agent is offline |

####  Target
  Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `type` | string | no | no | The trigger action target type. exp:[department,agent] |
  | `departments` | array | no | no | an integer array of  department id. |
  | `agents` | array | no | no | an integer  array of  agent id. |
  | `visitorSegmentId` | integer  | no | no | visitor Segment Id |

  ####  Order
  Action is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |
  | - | - | :-: | :-: | - |
  | `id` | integer | no | yes | The smarttrigger id  |
  | `position` | integer | no | yes |  The smarttrigger order number. |

### Smart Trigger End Points  
##### Get all smart triggers of the bot

  `GET /api/v1/bot/bots/{botId}/smartTriggers`
 
###### Parameters

 path parameters

 - `botId` 

####### Response    

 - Response: An array of  [TriggerRule](#triggerrule)  Object.
    
##### Get a smart trigger by id

  `GET /api/v1/bot/bots/{botId}/smartTriggers/{id}`

###### Parameters  

  path parameters

  - `botId` 
  - `id`

###### Response

  - Response:  [TriggerRule](#triggerrule) Object.
    
##### Create a new smart trigger

  `POST /api/v1/bot/bots/{botId}/smartTriggers`

###### Parameters

  path parameters

  - `botId` 

   request body parameters
  - [TriggerRule](#triggerrule) Object

###### Response

  the response is: [TriggerRule](#triggerrule) Object


##### Update a smart trigger

  `PUT /api/v1/bot/bots/{botId}/smartTriggers/{id}`
    
###### Parameters  
path parameters

  - `id`
  - `botId` 

 request body parameters
  - [TriggerRule](#triggerrule) Object

###### Response
      
  the response is [TriggerRule](#triggerrule) Object
    
##### Remove a smart trigger
 
  `DELETE /api/v1/bot/bots/{botId}/smartTrigger/{id}`
  
###### Parameters  
path parameters

  - `botId` 
  - `id`
      
###### Response   
the response is: Http Status Code `200`

##### Update the order of smart triggers

  `PUT /api/v1/bot/bots/{botId}/smartTriggers/order`
    
###### Parameters  
path parameters

  - `botId` 

 request body parameters
  - an array list of [Order](#Order) Object

###### Response
      
  the response is: Http Status Code `200`
    
##### Remove a smart trigger
 ## Quick Reply
  You need `Manage Bot` permission to manage Quick Reply and customize the settings for a Quick Reply.
  - `Quick Replies` - Quick Reply Manage
    + `GET /api/v1/bot/bots/{botId}/quickreplies` - [Get all quick replies of a bot](#get-all-quick-replies-of-a-bot)
    + `POST /api/v1/bot/bots/{botId}/quickreplies` - [Create a new quick reply](#create-a-new-quick-reply)
    + `GET /api/v1/bot/bots/{botId}/quickreplies/{id}` - [GET a quick reply](#get-a-quick-reply)
    + `PUT /api/v1/bot/bots/{botId}/quickreplies/{id}` - [Update a quick reply](#update-a-quick-reply)
    + `DELETE /api/v1/bot/bots/{botId}/quickreplies/{id}` - [Remove a quick reply](#remove-a-quick-reply)

### Quick Reply Json Format
#### Quick Reply Object
  Quick Reply is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the Quick Reply |
  | `name` | string  | no | yes | name of the Quick Reply |
  | `items` | list of [Quick Reply Item](#Quick-Reply-Item) Objects   | no | yes | the items of quick reply |

#### Quick Reply Item Object
 QuickReplyItem is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of Quick Reply item |
  | `type` | string  | no | yes | enum value, `goToIntent` and `contactAgent` |
  | `name` | string  | no | no | when item type is goToIntent, it is the name of the intent or it is empty string |
  | `intentId` | integer  | no | no | when item type is goToIntent, it is the id of the intent or it is 0 |

### Quick Reply End Points

#### Get all quick replies of a bot

  `GET /api/v1/bot/bots/{botId}/quickreplies`

##### Parameters
path parameters

  - `botId`

##### Response
the response is: list of [QuickReply](#quick-reply-object) Objects

#### Create a new quick reply

  `POST /api/v1/bot/bots/{botId}/quickreplies`

##### Parameters
path parameters

  - `botId` 

request body parameters: [QuickReply](#quick-reply-object) Object

##### Response
the response is: [QuickReply](#quick-reply-object) Object

## Get a quick reply

  `PUT /api/v1/bot/bots/{botId}/quickreplies/{id}`

##### Parameters
path parameters

  - `id`
  - `botId` 

##### Response
the response is: [QuickReply](#quick-reply-object) Object

## Update a quick reply

  `GET /api/v1/bot/bots/{botId}/quickreplies/{id}`

##### Parameters
path parameters

  - `id`
  - `botId` 

request body parameters: [QuickReply](#quick-reply-object) Object

##### Response
the response is: [QuickReply](#quick-reply-object) Object

#### Remove a quick reply

  `DELETE /api/v1/bot/bots/{botId}/quickreplies/{id}`

##### Parameters
path parameters

  - `botId` 
  - `id ` 

##### Response
the response is: Http Status Code `200`

## Learning Question
  You need `Manage Bot` permission to manage Learning Question and customize the settings for a Learning Question.
  - `Learning Questions` - Learning Question Manage
    + `GET /api/v1/bot/bots/{botId}/learningQuestions` - [Get all learning questions of a bot](#get-all-learning-questions-of-a-bot)
    + `DELETE /api/v1/bot/bots/{botId}/learningQuestions/{id}` - [Remove a learning question](#remove-a-learning-question)

### Learning Question Related Objects Json Format
#### LearningQuestion
  LearningQuestion is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Description |    
  | - | - | - | 
  | `id` | integer  | id of Learning Question |
  | `botName` | string  | name of the bot |
  | `chatId` | int  | id of the chat |
  | `question` | string  | visitor asked question |
  | `intentId` | int  | id of the intent |
  | `intentName` | string  | name of the intent |
  | `score` | double  | match score between the visitor question and itent. |
  | `rateType` | string  | enum type. `helpfull`, `notHelpfull`, `none` |
  | `answerType` | string  | enum type. `highConfidenceAnswer`, `possibleAnswer`, `noAnswer`, `none` |
  | `questionAskedTime` | datetime  | question asked time |

### Learning Question End Points
#### Get all learning questions of a bot

  `GET /api/v1/bot/bots/{botId}/learningQuestions`

##### Parameters
path parameters

  - `botId` 

query parameters

  - `timeFrom ` -query start time.
  - `timeTo ` -query end time.
  - `timezone ` -

##### Response

the response is: list of [LearningQuestion](#learningquestion) Objects

#### Remove a learning question

  `DELETE /api/v1/bot/bots/{botId}/learningQuestions/{id}`

##### Parameters
path parameters

  - `botId` 
  - `id ` 

##### Response
the response is: Http Status Code `200`

## report
  - `Reports` - Bot Manage
    + `GET /api/v1/bot/reports/chat` - [Chat report](#chat-report)
    + `GET /api/v1/bot/reports/answer` - [Answer report](#answer-report)
    + `GET /api/v1/bot/reports/highConfidenceAnswer` - [High confidence answer report](#high-confidence-answer-report)
    + `GET /api/v1/bot/reports/rating` - [Rating report](#rating-report)
    + `GET /api/v1/bot/reports/botAgent` - [Bot versus agent report](#bot-versus-agent-report)
    + `GET /api/v1/bot/reports/last7DaysSummary` - [Last 7 days summary report](#last-7-days-summary-report)
    + `GET /api/v1/bot/reports/7DaysDaily` - [Last 7 days daily report](#last-7-days-daily-report)
    + `GET /api/v1/bot/reports/export`  - [Export report by report type](#export-report-by-report-type)

### Report Related Object Json Format
#### ReportParameters
  ReportParameters is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `siteId` | integer  | no | yes | query site id |
  | `filterType` | string  | no | yes | Enum type,  `site`, `campaign`, `bot`, `facebookPage`, `twitterAccount` |
  | `filterValue` | string  | no | yes | value of the filter |
  | `timeFrom` | datetime  | no | yes | query start time |
  | `timeTo` | datetime  | no | yes | query end time |
  | `timeZone` | string  | no | yes | ±hh:mm, in the [TZ format](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones), defaults to UTC time |
  | `displayBy` | string  | no | yes | query type, it is a Enum. `day`, `week`, `month`. |
  | `dimensionType` | string  | no | yes | Enum type,  `byTime`,`allChannel`,`livechatChannel`,`facebookChannel`, `twitterChannel`. |

#### ChatReport
  ChatReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `totalBotResolved` | int  | no | yes |  |
  | `totalBotUnResolved` | int  | no | yes |  |
  | `totalBotTransferedAgent` | int  | no | yes |  |
  | `totalBotTransferredOfflineMessage` | int  | no | yes |  |
  | `dataList` | object  | no | yes | list of [ChatReportDetail](#chatreportdetail) Object  |

#### ChatReportDetail
  ChatReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `botResolved` | int  | no | yes |  |
  | `botUnResolved` | int  | no | yes |  |
  | `botTransferedAgent` | int  | no | yes |  |
  | `botTransferredOfflineMessage` | int  | no | yes |  |
  | `time` | datetime  | no | yes | statistical time |

#### AnswerReport
  AnswerReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `percentOfHighConfidenceAnswers` | int  | no | yes | percentage of high configdence answer |
  | `totalAnswers` | int  | no | yes | total answers count |
  | `totalHighConfidenceAnswers` | int  | no | yes | total high configdence answers count |
  | `totalNoAnswers` | int  | no | yes | total no answers count |
  | `totalPossibleAnswers` | int  | no | yes | total possible answers count |
  | `dataList` | object  | no | yes | list of [AnswerReportDetail](#answerreportdetail) Object  |

#### AnswerReportDetail
  AnswerReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `percentOfHighConfidenceAnswers` | int  | no | yes | percentage of high configdence answer |
  | `answers` | int  | no | yes | total answers count |
  | `highConfidenceAnswers` | int  | no | yes | total high configdence answers count |
  | `noAnswers` | int  | no | yes | total no answers count |
  | `possibleAnswers` | int  | no | yes | total possible answers count |
  | `time` | datetime  | no | yes | statistical time |

#### HighConfidenceReport
  HighConfidenceReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `totalHelpful` | int  | no | yes | high configdence answers count |
  | `totalHighConfidence` | int  | no | yes | total answers count |
  | `totalNoRate` | int  | no | yes | total high configdence answers count |
  | `totalNotHelpful` | int  | no | yes | total no answers count |
  | `dataList` | object  | no | yes | list of [HighConfidenceReportDetail](#highconfidencereportdetail) Object  |

#### HighConfidenceReportDetail
  HighConfidenceReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `helpful` | int  | no | yes | high configdence answers count |
  | `highConfidence` | int  | no | yes | total answers count |
  | `noRate` | int  | no | yes | total high configdence answers count |
  | `notHelpful` | int  | no | yes | total no answers count |
  | `time` | datetime  | no | yes | statistical time |

#### RatingReport
  RatingReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `avgScore` | int  | no | yes | average score |
  | `totalRatingTimes` | int  | no | yes | rating times |
  | `totalScore1Times` | int  | no | yes | the rating score is 1 times |
  | `totalScore2Times`  | int  | no | yes | the rating score is 2 times |
  | `totalScore3Times`  | int  | no | yes | the rating score is 3 times |
  | `totalScore4Times`  | int  | no | yes | the rating score is 4 times |
  | `totalScore5Times`  | int  | no | yes | the rating score is 5 times |
  | `dataList` | object  | no | yes | list of [RatingReportDetail](#ratingreportdetail) Object  |

#### RatingReportDetail
  RatingReportDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `avgScore` | int  | no | yes | average score |
  | `ratingTimes` | int  | no | yes | rating times |
  | `score1Times` | int  | no | yes | the rating score is 1 times |
  | `score2Times`  | int  | no | yes | the rating score is 2 times |
  | `score3Times`  | int  | no | yes | the rating score is 3 times |
  | `score4Times`  | int  | no | yes | the rating score is 4 times |
  | `score5Times`  | int  | no | yes | the rating score is 5 times |
  | `time` | datetime  | no | yes | statistical time |

#### BotAgentReport
  BotAgentReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `avgScore` | double  | no | yes | average score |
  | `avgTime` | double  | no | yes | average time |
  | `chats` | int  | no | yes | chats |
  | `agent` | object  | no | yes | list of [BotAgentReportDetail](#botagentreportdetail) Object  |
  | `bot` | object  | no | yes | list of [BotAgentReportDetail](#botagentreportdetail) Object  |

#### BotAgentReportDetail
  BotAgentReportBotDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `avgScore` | double  | no | yes | average score |
  | `avgTime` | double  | no | yes | average time |
  | `chats` | int  | no | yes | chats |
  | `time` | datetime  | no | yes | statistical time |

#### Last7DaysSummaryReport
  Last7DaysSummaryReport is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `averageRatingScore` | double  | no | yes | average rating score |
  | `botOnlyChatCount` | double  | no | yes | bot only chats count |
  | `botOnlyChatsTime` | double  | no | yes | bot only chats time |
  | `botAnswerCount` | double  | no | yes | bot answers count |
  | `chatsFromBotToAgentCount` | int  | no | yes | transferred from bot to agent chats count |
  | `percentageOfBotOnlyChats` | double  | no | yes | helpful answers count |
  | `percentageOfHighConfidenceAnswers` | double  | no | yes | percentage of high confidence answers |

#### Last7DaysDailyReport
  Last7DaysDaily is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `totalChatbotOnly` | int  | no | yes | total bot only chats count |
  | `totalFromBotToAgent` | int  | no | yes | total transferred from bot to agent chats count |
  | `totalPercentageOfBotOnlyChats` | double  | no | yes | total percentage of bot only chats |
  | `dataList` | object  | no | yes | list of [Last7DaysDailyReportDetail](#last7daysdailyreportdetail) Object  |

#### Last7DaysDailyReportDetail
  Last7DaysDailyDetail is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `chatbotOnly` | int  | no | yes | total bot only chats count |
  | `fromBotToAgent` | int  | no | yes | total transferred from bot to agent chats count |
  | `dailyChatsCount` | int  | no | yes | daily chats count |
  | `percentageOfBotOnlyChats` | double  | no | yes | total percentage of bot only chats |
  | `time` | datetime  | no | yes | statistical time |

### Report End Points  
#### Chat report

  `GET /api/v1/bot/reports/chat`

##### Parameters
query parameters: [ReportParameters](#reportparameters) Object

##### Response
the response is: [ChatReport](#chatreport) Object

#### Answer report

  `GET /api/v1/bot/reports/answer`

##### Parameters
query parameters: [ReportParameters](#reportparameters) Object

##### Response
the response is: [AnswerReport](#answerreport) Object

#### High confidence answer report

  `GET /api/v1/bot/reports/highConfidenceAnswer`

##### Parameters
query parameters: [ReportParameters](#reportparameters) Object

##### Response
the response is: [HighConfidenceReport](#highconfidencereport) Object
    
#### Rating report

  `GET /api/v1/bot/reports/rating`

##### Parameters
query parameters: [ReportParameters](#reportparameters) Object

##### Response
the response is: [RatingReport](#ratingreport) Object
    
#### Bot versus agent report

  `GET /api/v1/bot/reports/botAgent`

##### Parameters
query parameters: [ReportParameters](#reportparameters) Object

##### Response
the response is: [BotAgentReport](#botagentreport) Object
    
#### Last 7 days summary report

  `GET /api/v1/bot/reports/last7DaysSummary`

##### Parameters
query parameters: [ReportParameters](#reportparameters) Object

##### Response
the response is: [Last7DaysSummaryReport](#last7dayssummaryreport) Object
    
#### Last 7 days daily report

  `GET /api/v1/bot/reports/last7DaysDaily`

##### Parameters
query parameters: [ReportParameters](#reportparameters) Object

##### Response
the response is: [Last7DaysDailyReport](#last7daysdailyreport) Object
    
#### Export report by report type

  `GET /api/v1/bot/reports/export `

##### Parameters
query parameters

  - [ReportParameters](#reportparameters) Object
  - `reportType ` -Enum value: `chat`, `response`, `highConfidenceResponse`, `rating`, `botAgent`, `last7DaysDaily`
  
##### Response
the response is:

  - `fileName` -the excel report file full name
 
## General
  You need `Manage Bot` permission to manage General settings.
  - `General` 
    + `POST /api/v1/bot/file` - [Upload file temporarily, the file will be deleted in 3 hours](#upload-file-temporarily-and-the-file-will-be-deleted-in-3-hours)
    + `POST /api/v1/bot/image`  - [Upload image](#upload-image)
    + `POST /api/v1/bot/newBotRequest` - [Request to create a new bot](#request-to-create-a-new-bot)
    + `GET /api/v1/bot/botEnabled` - [Get if the site is enabled bot](#get-if-the-site-is-enabled-bot)
    + `GET /api/v1/bot/defaultAvatar` - [Get the default avatar of bot](#get-the-default-avatar-of-bot)
    + `GET /api/v1/bot/quota` - [Get used quotas and quota balance of a site](#get-used-quotas-and-quota-balance-of-a-site)
    + `GET /api/v1/bot/languages` - [Get all supported languages](#get-all-supported-languages)
    + `GET /api/v1/bot/operations/{id}` - [Get the operations such as import or train status](#get-the-operations-such-as-import-or-train-status)
    + `GET /api/v1/bot/prebuiltEntities` - [Get all Prebuilt Entities of a language](#get-all-prebuilt-entities-of-a-language)

#### PrebuiltEntity
  PrebuiltEntity is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `name` | integer  | no | yes | name of the prebuilt entity |
  | `displayName` | integer  | no | yes | display name of the prebuilt entity |
  | `description` | integer  | no | yes | description of the prebuilt entity |
  | `example` | integer  | no | yes |example of the prebuilt entity |

### General Related Object Json Format
#### NewBotRequest
  NewBotRequest is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `id` | integer  | yes | no | id of the New Bot Request |
  | `name` | string  | no | yes | name of the applier |
  | `email` | string  | no | yes | email of the applier |
  | `botName` | string  | no | yes | bot Name in the Requested bot |
  | `language` | string  | no | yes | bot language of the Requested bot |

#### MonthlyQuota
  MonthlyQuota is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `balance` | integer  | no | yes | the current month quota balance of the site |
  | `used` | integer  | no | yes | the current month used quotas of the site |

#### Language Object
  Language is represented as simple flat JSON objects with the following keys:  

  | Name | Type | Read-only | Mandatory | Description |    
  | - | - | :-: | :-: | - | 
  | `code` | string  | no | yes | the code of the Language |
  | `name` | string  | no | yes | the name of the Language |

### General End Points
#### Upload file temporarily and the file will be deleted in 3 hours

  `POST /api/v1/bot/file`

##### Parameters

query parameters

  - `siteId ` 

request body parameters

  - `file ` -the file content. it is a list

##### Response
the response is:

  - `fileName` -the uploaded file full name

#### Upload image

  `POST /api/v1/bot/image`

##### Parameters
request body parameters

  - `file ` -the file content. it is a list

##### Response
the response is: [NameUrl](#nameurl) Object

#### Request to create a new bot

  `POST /api/v1/bot/newBotRequest`

##### Parameters
query parameters

  - `siteId ` 

request body parameters: [NewBotRequest](#newbotrequest) Object

#### Get if the site is enabled bot

  `GET /api/v1/bot/botEnabled`

##### Parameters
query parameters

  - `siteId ` 

##### Response
the response is: 
  - `isEnabledBot ` 

#### Get the default avatar of bot

  `GET /api/v1/bot/defaultAvatar`

##### Parameters
no parameters

##### Response
the response is:  [NameUrl](#nameurl) Object

#### Get used quotas and quota balance of a site

  `GET /api/v1/bot/quota`

##### Parameters
query parameters

  - `siteId ` 

##### Response
the response is: [MonthlyQuota](#monthlyquota) Object
    
#### Get all supported languages

  `GET /api/v1/bot/languages`

##### Parameters
no parameters

##### Response
the response is: list of [Language](#language-object) Objects

#### Get the operations such as import or train status

  `GET /api/v1/bot/operations/{id}`

##### Parameters
path parameters

  - `id`

##### Response
the response is:

when the status is `Processing `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `operationId ` 

when the status is `Failed `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `
  - `failUrl ` 
  - `errorMessage ` 

when the status is `Succeeded `:

  - `status ` -enum values, `Succeeded `,`Failed `,`Processing `

#### Get all prebuilt entities of a language

  `GET /api/v1/bot/prebuiltEntities`

##### Parameters
path parameters

  - `languageCode`

##### Response
the response is: list of [Prebuilt Entity](#prebuiltentity) Objects    
