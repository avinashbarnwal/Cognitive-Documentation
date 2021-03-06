<!-- 
NavPath: Bing Speech API/Text To Speech
LinkLabel: API Reference
Url: Speech-api/documentation/API-Reference-REST/BingVoiceOutput
Weight: 180
-->
# Bing Text To Speech API

## Contents
[Introduction](#Introduction) 

[Voice Synthesis Request](#VoiceSynReq)
* [HTTP Headers](#Http) 
* [Input Parameters](#InputParam) 
* [Example Voice Output Request](#SampleVoiceOR) 

[Voice Output Responses](#VoiceOutResponse) 
  * [Successful Synthesis Response](#SuccessfulRecResponse) 
  * [Synthesis Failure](#RecFailure)
  * [Error Responses](#ErrorResponse) 

[Supported Locales and Voice Fonts](#SupLocales)  

[Troubleshooting and Support](#TrouNSupport)
 
## <a name="Introduction"> Introduction</a>

With the Bing Text to Speech API your application can send HTTP requests to a cloud server, where text is instantly synthesized into human sounding speech, and returned as an audio file.  The API can be used in many different contexts to provide real-time text to speech conversion in a variety of different voices and languages.  

## <a name="VoiceSynReq"> Voice Synthesis Request</a>

Clients must use the following end-point to access the service and build voice enabled applications: [https://speech.platform.bing.com/synthesize](https://speech.platform.bing.com/synthesize) 

Note! Until you have submitted your subscription key as described in [Bing Speech Recognition](./BingVoiceRecognition.md), this link will generate a 403 Response Error.

The API uses HTTP POST to send audio back to the client. The maximum amount of audio returned for a given request must not exceed 15 seconds. 
 
### <a name="Http">HTTP Headers</a>

HTTP headers for the request include:

Header   |Value  |Comments 
---------|---------|---------
Content-Type     |    application/ssml+xml     |      The input content type   
X-Microsoft-OutputFormat     |    **1)** raw-8khz-8bit-mono-mulaw, **2)** raw-16khz-16bit-mono-pcm, **3)** riff-8khz-8bit-mono-mulaw, **4)** riff-16khz-16bit-mono-pcm |       The output audio format  
X-Search-AppId     |    A GUID (hex only, no dashes)     |     An ID that uniquely identifies the client application. This can be Store ID for Apps. If one is not available, the ID may be user generated per-application.     
X-Search-ClientID     |     A GUID (hex only, no dashes)    |    An ID that uniquely identifies application instance per-installation.     
User-Agent     |     Application name    |     Application name is required and must be less than 255 characters.    

### <a name="InputParam">Input Parameters</a>
Inputs to the Bing Text to Speech API are expressed as HTTP query parameters. Parameters in the POST body are treated as Speech Synthesis Markup Language (SSML) content. Refer to the [SSML W3C Specification](http://www.w3.org/TR/speech-synthesis/) for a description of the markup used to control aspects of speech such as pronunciation, volume, pitch, rate, etc. 
The following is a complete list of recognized input parameters:  

**Note**: Unsafe characters should be escaped following the W3C URL specifications ([http://www.w3.org/Addressing/URL/url-spec.txt](http://www.w3.org/Addressing/URL/url-spec.txt)). 

**Note**: Requests with more than one instance of any parameter will result in an HTTP 400 error response.

###  <a name="SampleVoiceOR">Example Voice Output Request</a>

The following is an example of a voice output request:  
 
```
POST /synthesize
HTTP/1.1
Host: speech.platform.bing.com
Content-Type: audio/wav; samplerate=8000

X-Microsoft-OutputFormat: riff-8khz-8bit-mono-mulaw
Content-Type: text/plain; charset=utf-8
Host: speech.platform.bing.com
Content-Length: 197

<speak version='1.0' xml:lang='en-US'><voice xml:lang='en-US' xml:gender='Female' name='Microsoft Server Speech Text to Speech Voice (en-US, ZiraRUS)'>Microsoft Bing Voice Output API</voice></speak>
```
 
## <a name="VoiceOutResponse"> Voice Output Responses</a>

The API response contains the audio stream and the codec and will match the requested output format.
 
#### <a name="SuccessfulRecResponse"> Successful Synthesis Response</a>

Example JSON response for a successful voice search. The comments and formatting of the JSON below is for example reasons only. Indentation spaces, smart quotes, comments, etc. are omitted from the actual response. 
```
HTTP/1.1 200 OK
Content-Length: XXX
Content-Type: audio/x-wav 

Response audio payload       
```
 
#### <a name="RecFailure"> Synthesis Failure</a>

Example JSON response for a voice synthesis query failure.

```
HTTP/1.1 400 XML parser error
Content-Type: text/xml
Content-Length: 0
```
 
### <a name="ErrorResponse"> Error Responses</a>

Error   | Description 
---------|---------
**HTTP/400 Bad Request** | Will be returned if a required parameter is missing, empty or null, or if the value passed to either a required or optional parameter is invalid. The “Invalid” response includes passing a string value that is longer than the allowed length. A brief description of the problematic parameter will be included.  
**HTTP/401 Unauthorized** | Will be returned if the request is not authorized. 
**HTTP/413 RequestEntityTooLarge**  | Will be returned if the SSML input is larger than what is supported. 
**HTTP/502 BadGateway** | Network related problem or a server side issue. 

#### Example Error Response.
```
HTTP/1.0 400 Bad Request
Content-Length: XXX
Content-Type: text/plain; charset=UTF-8

Voice name not supported
```

## <a name="SupLocales">Supported Locales and Voice Fonts</a>

Supported locales and related voice fonts include:

Locale | Gender | Service name mapping 
---------|--------|------------
ar-EG*   |   Female  | "Microsoft Server Speech Text to Speech Voice (ar-EG, Hoda)"
de-DE    |   Female  | "Microsoft Server Speech Text to Speech Voice (de-DE, Hedda)" 
de-DE    |   Male    | "Microsoft Server Speech Text to Speech Voice (de-DE, Stefan, Apollo)" 
en-AU    |   Female  | "Microsoft Server Speech Text to Speech Voice (en-AU, Catherine)" 
en-CA    |   Female  | "Microsoft Server Speech Text to Speech Voice (en-CA, Linda)"
en-GB    |   Female  | "Microsoft Server Speech Text to Speech Voice (en-GB, Susan, Apollo)"
en-GB    |     Male  | "Microsoft Server Speech Text to Speech Voice (en-GB, George, Apollo)"
en-IN    |     Male  | "Microsoft Server Speech Text to Speech Voice (en-IN, Ravi, Apollo)"  
en-US    |Female|"Microsoft Server Speech Text to Speech Voice (en-US, ZiraRUS)"
en-US    |Male|"Microsoft Server Speech Text to Speech Voice (en-US, BenjaminRUS)"
es-ES    |Female|"Microsoft Server Speech Text to Speech Voice (es-ES, Laura, Apollo)"
es-ES    |Male|"Microsoft Server Speech Text to Speech Voice (es-ES, Pablo, Apollo)"
es-MX|Male|"Microsoft Server Speech Text to Speech Voice (es-MX, Raul, Apollo)"
fr-CA|Female|"Microsoft Server Speech Text to Speech Voice (fr-CA, Caroline)"
fr-FR|Female|"Microsoft Server Speech Text to Speech Voice (fr-FR, Julie, Apollo)"
fr-FR|Male|"Microsoft Server Speech Text to Speech Voice (fr-FR, Paul, Apollo)"
it-IT|Male|"Microsoft Server Speech Text to Speech Voice (it-IT, Cosimo, Apollo)"
ja-JP|Female|"Microsoft Server Speech Text to Speech Voice (ja-JP, Ayumi, Apollo)"
ja-JP|Male|"Microsoft Server Speech Text to Speech Voice (ja-JP, Ichiro, Apollo)"
pt-BR|Male|"Microsoft Server Speech Text to Speech Voice (pt-BR, Daniel, Apollo)"
ru-RU|Female|"Microsoft Server Speech Text to Speech Voice (ru-RU, Irina, Apollo)"
ru-RU|Male|"Microsoft Server Speech Text to Speech Voice (ru-RU, Pavel, Apollo)"
zh-CN|Female|"Microsoft Server Speech Text to Speech Voice (zh-CN, HuihuiRUS)"
zh-CN|Female|"Microsoft Server Speech Text to Speech Voice (zh-CN, Yaoyao, Apollo)"
zh-CN|Male|"Microsoft Server Speech Text to Speech Voice (zh-CN, Kangkang, Apollo)"
zh-HK|Female|"Microsoft Server Speech Text to Speech Voice (zh-HK, Tracy, Apollo)"
zh-HK|Male|"Microsoft Server Speech Text to Speech Voice (zh-HK, Danny, Apollo)"
zh-TW|Female|"Microsoft Server Speech Text to Speech Voice (zh-TW, Yating, Apollo)"
zh-TW|Male|"Microsoft Server Speech Text to Speech Voice (zh-TW, Zhiwei, Apollo)"
 *ar-EG supports Modern Standard Arabic (MSA)

## <a name="TrouNSupport"> Troubleshooting and Support</a>

Post all questions and issues to the [Bing Speech Service](https://social.msdn.microsoft.com/Forums/en-US/home?forum=SpeechService) MSDN Forum, with complete detail, such as: 
* An example of the full request string (minus the raw audio data).
* If applicable, the full output of a failed request, which includes log IDs.
* The percentage of requests that are failing.

