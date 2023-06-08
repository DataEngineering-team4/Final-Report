## The Team

-   Kangbeen Ko
-   Minjun Kim
-   Yoonjae Kim
-   Taejun Eom

Github Organization: [https://github.com/DataEngineering-team4](https://github.com/DataEngineering-team4)

## Problem Definition

In today's digital age, more and more children are exposed to smartphones at an early age. At the same time, there is a remarkable trend of reduced interpersonal communication, which is being overshadowed by personal content consumption. In particular, positive social exchanges are significantly reduced for dual-income families or long-term hospitalized children. This is an important issue because limited conversation can degrade children's communication skills.

To solve this problem, we developed an application that helps children develop their communication skills. The app allows children to have voice conversations with their own animated characters. Basically, it provides a unique companion for children to talk to when they lack a contact or when their parents are unable to participate in the conversation with them.

This application is designed to solve the problem of reduced conversation between children. According to a 2017 study published in the Journal of Developmental and Behavior Pediatrics[1], children who spend more time with portable screens are more likely to delay speaking. Similarly, a report by the British Communications Trust [2] suggests that children's language development is hampered by screen-driven lifestyles and lack of conversation at home. Our application aims to alleviate this problem by providing an interactive and attractive way for children to practice and develop conversational skills.


### Video Demo

https://github.com/DataEngineering-team4/Final-Report/assets/76294398/97bfae38-b82c-4b19-8532-ee4f3f123651


## System Design

Our system can be broken down into three primary components: 

1. Mobile Application: Developed with Flutter (Dart), this application is the primary user interface. It allows users to interact with their custom animated characters using their voice.

2. Backend System: Hosted on AWS EC2, this system is built using Django Rest Framework (DRF). It serves as the intermediary between the mobile application and the Inference Server, processing user voice data and relaying it to and from the relevant services.

3. Inference Server: Hosted on a separate server, this system houses our fine-tuned Text-to-Speech (TTS) model. It converts text responses from the ChatGPT API into voice data.

Here's a brief overview of how these components interact:

1. The user inputs voice data(waveform) through the mobile application.

2. The voice data is sent to the Backend System.

3. The Backend System uses the OpenAI Whisper API to convert the voice data into text.

4. This text data is then inputted into the ChatGPT API to generate a text response.

5. The response text is sent to the Inference Server, which uses the TTS model to convert it into voice data.

6. The voice data is sent back to the Backend System, which relays it to the Mobile Application.

7. The user then receives the voice response through the mobile application.

This design allows for efficient interaction between the user and the system, promoting real-time conversation with the animated character.



## Broader Impact

## Reflections

## References

1.   Madigan, Sheri, et al. (2017). Association Between Screen Time and Children’s Performance on a Developmental Screening Test. Journal of the American Medical Association Pediatrics, [https://jamanetwork.com/journals/jamapediatrics/fullarticle/2664947](https://jamanetwork.com/journals/jamapediatrics/fullarticle/2664947)
2.   The Communication Trust, “Talk of the Town”, [https://www.thecommunicationtrust.org.uk/resources/resources/resources-for-practitioners/talk-of-the-town/](https://www.thecommunicationtrust.org.uk/resources/resources/resources-for-practitioners/talk-of-the-town/)
