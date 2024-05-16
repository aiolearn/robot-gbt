# Build chatGPT and voice processing

In this project, we have written a GBT chat robot program that asks questions through voice and answers us.

## Modules

```python
import openai
import requests as req 
import IPython
from audioplayer import AudioPlayer
import speech_recognition as sr 
```

## Usage

We use API key for this program

```python
openai.api_key = "your api_key"
```

This code is a Python program that uses the SpeechRecognition library for audio capture and recognition, and the OpenAI API for generating textual responses. Here's an explanation of its components:

1. **Speech Recognition**:
   - The code creates a speech recognition object with `sr.Recognizer()`.
   - It uses `sr.Microphone()` to capture audio from the microphone, storing the captured audio in a variable called `audio`.
   - The `pause_threshold` parameter determines the time duration of silence that triggers the end of recording.

2. **Speech-to-Text Conversion**:
   - Using `recognize_google()`, the code converts the captured audio into text. The language for recognition is set to "fa-IR" (Persian).
   - After the audio is converted to text, the recognized text is stored in a variable named `query`.

3. **Getting a Response from OpenAI API**:
   - The `query` variable, containing the recognized text, is sent as input to the OpenAI API.
   - The `openai.Completion.create()` function is used to generate a textual response from the GPT model. Parameters like `engine` (to choose the model), `prompt` (the input text), `max_tokens` (maximum number of tokens for the response), and `temperature` (controls response creativity) are configured.
   - The generated response from the OpenAI API is stored in a variable named `javab`.

4. **Generating Audio from Text (Commented-out code)**:
   - The commented-out section indicates that the program might convert the textual response into audio.
   - A TTS (Text-to-Speech) service is used. An HTTP request with parameters such as the response text and language is sent to the service.
   - The content of the audio response is saved to a file named `stream.mp3`.
   - An audio player is used to play this audio file.

Overall, this code demonstrates a complete process of capturing audio, converting speech to text, getting a response from the OpenAI API, and then optionally generating an audio response for playback.

```python
r = sr.Recognizer()
with sr.Microphone() as source: 
     r.pause_threshold = 1
     audio = r.listen(source)


print("در حال پردازش صدا")
query = r.recognize_google(audio, language ='fa-IR')
print("سوال شما: ",query)

soal = query

robot = openai.Completion.create(
    engine="text-davinci-003",
    prompt=soal,
    max_tokens=1024,
    n=1,
    stop=None,
    temperature=0.9,
)
 
javab = robot.choices[0].text

# jabab=javab.replace("؟"," ")
# jabab=javab.replace("\\r\\n", "")
print(javab)
# tts=javab
# r = req.get("https://one-api.ir/tts/?token=843530:64144825a027e&action=microsoft&lang=fa-IR-FaridNeural&q="+tts, stream=True)

# with open('stream.mp3', 'wb') as f:
#     try:
#         for au in r.iter_content(1024):
#             f.write(au)
        
#     except KeyboardInterrupt:
#         pass

# AudioPlayer("stream.mp3").play(block=True)
```

## Result

This project was written by Majid Tajanjari and the Aiolearn team, and we need your support!❤️

# ساخت chatGPT و صدا processing

در این پروژه یک برنامه ربات چت GBT نوشته ایم که از طریق صدا سوال می پرسد و به ما پاسخ می دهد.

## ماژول ها

```python
import openai
import requests as req 
import IPython
from audioplayer import AudioPlayer
import speech_recognition as sr 
```

## نحوه استفاده

برای این برنامه از کلید API استفاده می کنیم

```python
openai.api_key = "your api_key"
```

این کد یک برنامه پایتون است که از کتابخانه‌های SpeechRecognition برای ضبط و تشخیص صدا و OpenAI API برای ایجاد پاسخ‌های متنی استفاده می‌کند. در ادامه توضیح مراحل آن آمده است:

1. **تشخیص صدا**:
   - کد از `sr.Recognizer()` برای ایجاد یک شیء تشخیص صدا استفاده می‌کند.
   - از `sr.Microphone()` برای ضبط صدای ورودی از میکروفون استفاده می‌شود. صدایی که از میکروفون ضبط می‌شود، در متغیری به نام `audio` ذخیره می‌شود.
   - `pause_threshold` به منظور تعیین مدت زمانی که پس از آن توقف، ضبط صدا متوقف می‌شود، تنظیم شده است.

2. **تشخیص گفتار و پردازش**:
   - با استفاده از `recognize_google()`، کد صدای ضبط‌شده را به متن تبدیل می‌کند. زبان تشخیص "fa-IR" (فارسی) است.
   - پس از تبدیل صدا به متن، متن تشخیص‌داده‌شده در متغیری به نام `query` ذخیره می‌شود.

3. **پاسخ به سوال با OpenAI API**:
   - متغیر `query` که شامل متن است، به عنوان ورودی به OpenAI API ارسال می‌شود.
   - `openai.Completion.create()` برای ایجاد یک پاسخ متنی از مدل GPT استفاده می‌شود. پارامترهایی مثل `engine` (برای انتخاب مدل)، `prompt` (متن ورودی)، `max_tokens` (حداکثر تعداد توکن‌ها در پاسخ)، و `temperature` (کنترل خلاقیت پاسخ) تنظیم شده‌اند.
   - پاسخ تولیدشده توسط OpenAI API در متغیری به نام `javab` ذخیره می‌شود.

4. **تولید فایل صوتی (کدهای کامنت‌شده)**:
   - بخش کامنت‌شده نشان می‌دهد که ممکن است برنامه بخواهد پاسخ متنی را به صدا تبدیل کند.
   - از یک سرویس TTS (تبدیل متن به صدا) استفاده می‌شود. درخواست HTTP با پارامترهایی مثل متن پاسخ و زبان به سرویس ارسال می‌شود.
   - محتوای پاسخ صوتی در یک فایل به نام `stream.mp3` ذخیره می‌شود.
   - از یک پخش‌کننده صوتی برای پخش این فایل استفاده می‌شود.

به طور کلی، این کد فرآیند کامل دریافت صدا، تشخیص گفتار، دریافت پاسخ از OpenAI API، و سپس پخش پاسخ به صورت صوتی را نشان می‌دهد.
```python
r = sr.Recognizer()
with sr.Microphone() as source: 
     r.pause_threshold = 1
     audio = r.listen(source)


print("در حال پردازش صدا")
query = r.recognize_google(audio, language ='fa-IR')
print("سوال شما: ",query)

soal = query

robot = openai.Completion.create(
    engine="text-davinci-003",
    prompt=soal,
    max_tokens=1024,
    n=1,
    stop=None,
    temperature=0.9,
)
 
javab = robot.choices[0].text

# jabab=javab.replace("؟"," ")
# jabab=javab.replace("\\r\\n", "")
print(javab)
# tts=javab
# r = req.get("https://one-api.ir/tts/?token=843530:64144825a027e&action=microsoft&lang=fa-IR-FaridNeural&q="+tts, stream=True)

# with open('stream.mp3', 'wb') as f:
#     try:
#         for au in r.iter_content(1024):
#             f.write(au)
        
#     except KeyboardInterrupt:
#         pass

# AudioPlayer("stream.mp3").play(block=True)
```

## نتیجه

این پروژه توسط مجید تجن جاری و تیم Aiolearn نوشته شده است و ما به حمایت شما نیازمندیم!❤️