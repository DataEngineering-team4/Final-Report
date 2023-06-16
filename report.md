## Team information
<a href='https://kevintherainmaker.github.io/'>Kangbeen Ko </a>
- Project Ideation
- Model Research
- ML Engineering
- Model Serving
- Demo-day Presentation

Minjun Kim 
- Backend Development
- Whisper API Implementation
- Service Deployment

<a href='https://y00njaekim.github.io'>Yoonjae Kim </a>
- Project Ideation
- Backend Development
- Frontend Development
- UI/UX Design

Taejun Eom 
- Frontend Development
- Animated Drawing Implementation

## Problem definition
In today's digital age, more and more children are exposed to smartphones at an early age. At the same time, there is a remarkable trend of reduced interpersonal communication, which is being overshadowed by personal content consumption. In particular, positive social exchanges are significantly reduced for dual-income families or long-term hospitalized children. This is an important issue because limited conversation can degrade children's communication skills.
To solve this problem, we developed an application that helps children develop their communication skills. The app allows children to have voice conversations with their own animated characters. Basically, it provides a unique companion for children to talk to when they lack a contact or when their parents are unable to participate in the conversation with them.
This application is designed to solve the problem of reduced conversation between children. According to a 2017 study published in the Journal of Developmental and Behavior Pediatrics[1], children who spend more time with portable screens are more likely to delay speaking. Similarly, a report by the British Communications Trust [2] suggests that children's language development is hampered by screen-driven lifestyles and lack of conversation at home. Our application aims to alleviate this problem by providing an interactive and attractive way for children to practice and develop conversational skills.

## System design
Our system can be broken down into three primary components:
Mobile Application: Developed with Flutter (Dart), this application is the primary user interface. It allows users to interact with their custom animated characters using their voice.
Backend System: Hosted on AWS EC2, this system is built using Django Rest Framework (DRF). It serves as the intermediary between the mobile application and the Inference Server, processing user voice data and relaying it to and from the relevant services.
Inference Server: Hosted on a separate server, this system houses our fine-tuned Text-to-Speech (TTS) model. It converts text responses from the ChatGPT API into voice data.

Here's a brief overview of how these components interact:
1.	The user inputs voice data(waveform) through the mobile application.
2.	The voice data is sent to the Backend System.
3.	The Backend System uses the OpenAI Whisper API to convert the voice data into text.
4.	This text data is then inputted into the ChatGPT API to generate a text response.
5.	The response text is sent to the Inference Server, which uses the TTS model to convert it into voice data.
6.	The voice data is sent back to the Backend System, which relays it to the Mobile Application.
7.	The user then receives the voice response through the mobile application.
This design allows for efficient interaction between the user and the system, promoting real-time conversation with the animated character.

## Machine learning components
We used a TTS model that converts text into speech. The model consists of a Text-to-Mel module that converts text sequences into Mel-spectrograms and a Vocoder module that converts this Mel-spectrogram into voice signals.
First, FastSpeech2, a model with an encoder-decoder structure based on a feedforward transformer, was used as the Text-to-Mel module. The Variation adapter between the encoder and decoder adds voice features such as duration, pitch, and energy of speech to hidden sequences. By using this, it can reproduce the characteristics of speech used in training well.
We basically used Korean Single Speech (KSS) Dataset for training, and we can also fine-tune it with user data to change the voice.
We then used GAN-based MB-MelGAN as a vocoder module to enable lightweight and fast speech synthesis.

## Application demonstration
This app allows users to sign up or log in and engage in conversations with a default character provided. Upon launching the app, users are prompted to either register a new account or log in if they already have one. The app features a character that users can select and interact with through conversation.
There is a recording button in the app. Users can simply press the recording button, speak their desired message, and the character will respond accordingly. This creates a dialogue experience within the app.
Furthermore, when users upload a still image of their hand-drawn character, the app animates it to create movements. This allows users to engage in conversations with the animated character. By leveraging this feature, users can interact with their own custom characters in a dynamic and engaging way.
Additionally, users have the option to add a new character of their own. By selecting the "Add Character" button on the character selection screen, users can upload their own hand-drawn or designed character along with its name. After a certain period of time, the user's character becomes available for conversation within the app.
In summary, this app enables users to create an account, interact with a default character, engage in conversations, and even personalize their experience by adding their own characters.

https://github.com/DataEngineering-team4/Final-Report/assets/76294398/b9653a42-966b-47cd-b94e-f21b75428212

## Reflection
Firstly, we were able to successfully develop a text-to-speech (TTS) model that converts sentences into natural human language. However, we didn't have enough time to complete the fine-tuning of a model that would convert users' voices into personalized TTS. Given more time, I believe we could have accomplished this. In that case, parents could have recorded their voices to have more familiar conversations with their children.
Initially, our plan was to create an app where users could interact with popular characters like Pororo. However, we learned that this approach would violate copyright laws, preventing us from officially distributing the app. Consequently, we shifted our strategy. Users can now draw their own characters and animate them to engage in conversations. We utilized the animated drawings API from Meta, enabling users to have an enjoyable experience with our app.

If we had more resources and time, our priority would be reducing the latency of the TTS system. Currently, there is a significant delay between when users record their voice and when they receive a response, which could lead to user disengagement. Additionally, we plan to refine the prompts for the ChatGPT system. Due to limited efforts in prompt engineering, we couldn't optimize it effectively. However, we intend to save prompts differently for each user and character, capturing and processing conversations between users and ChatGPT to modify prompts accordingly. This way, each user and character will have a unique personality and charm, providing a more enjoyable experience for users.
If we had more time and resources, I agree that it would be beneficial to add a feature where the character's movements align with their responses, rather than having random animations. For example, when the user says "hello," the character could wave their hand, or when the user expresses positivity, the character could jump around energetically. Similarly, if the character becomes angry, they could show animation of clenched fists. Currently, there is a disconnect between the character's animations and their speech, and improving this synchronization would enhance the overall user experience.

## Broader impact
However, there are potential concerns associated with excessive use of our app. Users might spend too much time conversing with the app and neglect real-life social interactions with friends. Additionally, the storage of users' voices raises the risk of potential data breaches, exposing users' personal information or enabling the creation of inappropriate TTS outputs.
Apart from these concerns, I don't anticipate any significant negative impacts. However, we should be mindful of potential issues similar to what occurred with Eluda, where children expressed violent behavior towards characters within the app. It is possible that some users, particularly minors, may draw characters that engage in verbal abuse, bullying, or exhibit violent tendencies. Moreover, if the prompts for the ChatGPT system are not properly managed, there is a risk of receiving violent or aggressive responses from the model.
Therefore, it is crucial to implement measures to ensure responsible and safe usage of our app, including moderation, user guidelines, and privacy protection protocols.
