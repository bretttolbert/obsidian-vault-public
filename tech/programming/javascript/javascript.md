# javascript

###### Text to speech

```javascript
function speak(text) {
    console.log(text);
    voices = speechSynthesis.getVoices();
    console.log(voices);
    if (voices) {
        //English (Great Britain)+Robert
        //English (America)+Michael
        //English (Scotland)+Robosoft4
        //English (America)+RicishayMax
        //English (Scotland)+Steph
        voice = voices[65];
        for (const v of voices) {
            if (v.name == "English (Scotland)+Robosoft4") {
                voice = v;
                break;
            }
        }
        console.log(voice);
        var speech = new SpeechSynthesisUtterance(text);
        speech.voice = voice;
        window.speechSynthesis.speak(speech);
    } else {
        console.log("Failed to get voices");
        return;
    }
}
```
