import speech_recognition as sr
import cv2
import os
import webbrowser
import pywhatkit
import datetime
import wikipedia
import openai
import pyttsx3
import requests
import smtplib
from ultralytics import YOLO
from bs4 import BeautifulSoup
#from dotenv import load_dotenv
from gtts import gTTS
import numpy as np

# Initialize the speech engine and recognizer
engine = pyttsx3.init()
recognizer = sr.Recognizer()

def say(text):
    engine.say(text)
    engine.runAndWait()
def wishMe():
    say("Jai shree RAM!")
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        say("Good Morning Sir!")
 
    elif hour>=12 and hour<18:
        say("Good Afternoon Sir!")  
    else:
        say("Good Evening Sir!")  
def takeCommand():
    r= sr.Recognizer()
    with sr.Microphone() as source:
        r.pause_threshold = 1
        audio = r.listen(source)
        try:
            print("Recogniging..")
            query = r.recognize_google(audio, language="en-in")
            print(f"User said:{query}")
            return query
        except Exception as e:
            return "some error Occurred.sorry from me "
#def detect():
   # response = requests.get()
    #soup = BeautifulSoup(response.text

# Load the pre-trained object detector

def chat(query):
    url = f"https://www.google.com/search?qchat+{query}"
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    info = soup.find("div", class_="BNeawe iBp4i AP7Wnd").text
    desc = soup.find("div", class_="BNeawe tAd8D AP7Wnd").text
    return f"The information about {query} is{info}. {desc} "

def amazon(query):
    url = f"https://www.amazon.com/search?qamazon+{query}"
    response = requests.get(url)
    soup = gTTS(response.text, "html.parser")
    info = soup.find("div", class_="BNeawe iBp4i AP7Wnd").text
    desc = soup.find("div", class_="BNeawe tAd8D AP7Wnd").text
    return f"The information about {query} is {info}. {desc} "
# Define a function to get the weather information
def weather(city):
    url = f"https://www.google.com/search?q=weather+{city}"
    response = requests.get(url)
    soup = BeautifulSoup(response.text, "html.parser")
    temp = soup.find("div", class_="BNeawe iBp4i AP7Wnd").text
    desc = soup.find("div", class_="BNeawe tAd8D AP7Wnd").text
    return f"The temperature in {city} is {temp}. {desc}"
def sendEmail(to, content):
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('youremail@gmail.com', 'your-password')
    server.sendmail('youremail@gmail.com', to, content)
    server.close()
wishMe()
say(f" Hello!,I am jarvis ,what can i do for you")
while True: 
    print("listening..")
    query=takeCommand()
    if "Jarvis wake up" in query:
     say(f"Yes Boss, How can i help you") 
    elif "how are you" in query:
        say(f"I am good Boss!, What abut you ")
    sites = [["youtube","https://youtube.com"],["wikipedia","https://www.wikipedia.com"],["google","https://google.com"],["instagram","https://www.instagram.com"],
             ["whatsapp","https://www.whatsapp.com"],["tradingview","https://in.tradingview.com"],["stock","https://groww.in/stocks/user/explore"],["facebook","https://www.facebook.com"],
             ["live score","https://www.cricbuzz.com"],["hotstar","https://www.hotstar.com/in/home"],["movies 1","https://dotmovies.yachts"],["pinterest","https://www.pinterest.com"]]
    for site in sites:
        if f"Open {site[0]}".lower() in query.lower():
            say(f"opening {site[0]} sir..")
            webbrowser.open(site[1])
    if "play" in query:
        song = query.replace("play", "")
        say(f"Playing {song}")
        pywhatkit.playonyt(song)
    if "program" in query:
         code = query.replace("program", "")
         say(f"writing{code}")
         pywhatkit.program(code)
    if "amazon" in query:
         item = query.replace("amazon", "")
         say(f"searching {item} on googlesearch")
         info = gTTS.summary(topic, 1)
         say(info)
    if "the time" in query:
        strfTime = datetime.datetime.now().strftime("%H:%M:%S")
        say(f"Sir the time is {strfTime}")
    elif "weather" in query:
            city = query.replace("weather", "")
            say(f"Getting the weather information for {city}")
            info = weather(city)
            say(info)
    elif 'email to friend' in query:
            try:
                say("What should I say?")
                content = takeCommand()
                to = "yourfriendEmail@gmail.com"   
                sendEmail(to, content)
                say("Email has been sent!")
            except Exception as e:
                print(e)
                say("Sorry. I am not able to send this email")
    elif"chat" in query:
            topic = query.replace("chat", "")
            say(f"Chatting with you about {query}")
            info = wikipedia.summary(topic, 1)
            say(info)
    if "Jarvis Sleep".lower() in query.lower():
        say("okay , goodbye!")
        exit()
