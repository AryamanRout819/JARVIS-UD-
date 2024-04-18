# JARVIS-UD-
This is a jarvis raw code and this is still not implemented in OOPS .
import pyttsx3
import speech_recognition as sr
import pyaudio
import datetime
import webbrowser
import wikipedia
import os
import smtplib



engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')

engine.setProperty('voices', voices[0].id)


def speak(audio):
    engine.say(audio)
    print(audio)
    engine.runAndWait()
def wish_me():
    hour = int(datetime.datetime.now().hour)
    if 0 <= hour < 12:
        speak("Good morning!")
    elif 12 <= hour < 18:
        speak("Good afternoon!")
    else:
        speak("Good evening!")
    speak("iam jarvis sir , please tell me how may i help you")



def takecommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        speak("listening")
        r.pause_threshold = 3
        audio = r.listen(source, timeout=3, phrase_time_limit=5)

    try:
        print("Recognizing...")
        speak("Recognizing")
        query = r.recognize_google(audio, language='en-in')
        print(f"User said: {query}")
        return query

    except sr.UnknownValueError:
        print("Sorry, I didn't catch that.")
        speak("Sorry, I didn't catch that. Could you please repeat?")
        return "none"

    except sr.RequestError as e:
        print(f"Could not request results from Google Web Speech Recognition service; {e}")
        speak("Sorry, there was an issue with the speech recognition service.")
        return "none"
    return query

def send_email(to, content):
    server = smtplib.SMTP("smtp.gmail.com", 587)
    server.ehlo()

    server.starttls()
    server.login("aryamanrout.2819@gmail.com")
    server.sendmail("aryamanrout.2819@gmail.com", to, content)
    server.close()



if __name__=="__main__":

    wish_me()
    while True:

        query = takecommand().lower()
        if 'who am i' in query:
            speak("Aryaman Rout, studying in DAV Pokhariput, lives in Pristine Greens. He has many hobbies and enjoys playing games.")
            continue

        if 'thank you' in query:
            speak("You're welcome!")
            continue

        if 'sleep' in query:
            speak("Going to sleep. Wake me up when you need assistance.")
            break

        if 'who are you' in query:
            speak("")
        
            
        if 'wikipedia' in query:
            speak("Searching Wikipedia...")
            query = query.replace("Wikipedia" , "")
            results = wikipedia.summary(query , sentences = 2)
            speak("According to wikipedia")
            print(results)
            speak(results)

        elif 'open youtube' in query:
            webbrowser.open("youtube.com")

       

        elif 'Thank you ' in query:
            speak("Your welcome sir . Any other Query")

        elif 'open Goggle' in query:
            webbrowser.open("https://www.google.com/")

        elif 'open github' in query:
            webbrowser.open("https://github.com/")


        elif 'play music ' in query:
            music_dir= 'D:\\Aryaman folder (personal)\\Songs'

            songs = os.listdir(music_dir)
            print(songs)
            os.startfile(os.path.join(music_dir , songs[0]))

        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"sir, The time is : {strTime}")

        elif 'open code' in query:
            codepath = " C:\\Users\\Aryaman\\AppData\\Local\\Programs\\Microsoft VS Code"

            os.startfile(codepath)

        
        
