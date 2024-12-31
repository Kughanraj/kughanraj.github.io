---
layout: post
title: CyberX Writeup
date: 2024-12-31 22:53 +0800
categories: [CTF, Writeup]
tags: [ctf,writeup,cyberx,cybersentinels]
---

# Welcome to my Challenges Writeup for the CyberX CTF.

I know it is a bit late but here is my writeup for the challenges

## Forensic
Made quite alot of challenges in this cateogry since this is my **favourite** caterogy. 

>The challenges are:

### 1. Forensic Odyssey 1: A Message in the Mist
   Description: 
   The hacker left a taunting message for whoever dared investigate. It’s somewhere on the disk, lying in plain sight. Can you find the first piece of the puzzle?

   So for this challenge, I have given a .E01 file with 7gb size 💀

   The hardest part of this challenge is getting the .E01 file. After downloading the file, open FTK imager, navigate to File, press add evidence item and choose the image file option.
   
  ![Step1](images/1.1.png)

   Then press on the file until you enter the root folder. The scroll until the end and you will see the welcome.txt with the flag for this challenge.

   ![Step2](images/1.2.png)

   FLAG = CyberX{l3mm3_gu3ss_FTK?}

   Eazy Peazy Lemon Squezy right?

### 2. Forensic Odyssey 2: The Hidden Path
   Description: Hackers rarely leave their secrets in plain sight. This one is no different. Somewhere in the evidence is a hidden message—visible only to those who know where to look. Can you uncover it?

   Now this is the challenge where alot of you struggled, even though you guys already found the flag just could not see it. There were few people even opened ticket who found the 3rd and 4th flag but not this. 
   So let's see what is the **hidden message-visible only to those who know** means.

   So just like normal, we all know that people keep their documents in Users(default) folder. So rather than wasting time, going through all the files, let's analyze this folder only (I know everyone just looked through every file there is for the flag 💀.)

   Under Users only 1 user seems legit, which is plssk, so start analyze his files.
   Under his downloads folder, there is a weird folder name hidden, open the folder and voila we could see the flag2.txt.

   ![Step1](images/2_1.png)
   
   Upon opening the file, we are welcomed by a "Where is the flag???". So like any other sane person we should just search for it in other place right? ❌❌❌
   Next time when you receive a file like this, with nothing shown try "CTRL+A" to select all the thing in the file and see if there are anything else or is it really empty. 

   Now if you do "CTRL+A" to this file, you will see something like this.

   ![Step2](images/2_2.png)

   Now we know that there is something there, upload it into [dcode](https://dcode.fr/en). One of the most important tool for decryption alongside [cybcerchef](https://gchq.github.io/CyberChef/)

   Now copy the invisible characters from the file with "CTRL+A" + "CTRL+C" and paste it into dcode. After a bit of loading, there will be this ```Need to decrypt a message? Try our cipher identifier!``` sentence, press the cipher identifier and paste back the copied stuff into the ```ciphertext to recognize```. 


   ![Step3](images/2_3.png)

   Now press analyze and you will see the Results showing a lot of hits for the WhiteSpace Language. 
   Press the WhiteSpace Language and paste it back and and press decrpyt. Voila you will get the flag. 

   ![Step4](images/2_4.png)

   FLAG = CyberX{y0u_c4n_r34d_th1s?} 

### 3. Forensic Odyssey 3: The Time Traveler 
   Descrption: You’ve uncovered part of the trail, but there’s a gap in the story. The hacker tried to cover their tracks. Can you figure out what is missing?

   Hint for this challenge is the words ```gap in the story```. So most probably the hacker deleted the file. Just go to Recylce Bin in FTK imager and get the flag. 

   ![Step1](images/3_1.png)

   FLAG = CyberX{g3tt1ng_th3_g1st_0f_1t?}

### 4. Forensic Odyssey 4: The Final Trail
   Description: Something doesn’t sit right. Amidst all the recovered evidence, the number of pictures... smell fishy. You’ve learned to trust your instincts by now—there’s more to these images than meets the eye.

   Alright, I think no one actually solve this challenge the intended way since I know all of you would rather bruteforce check for all the file rather than reading the description.

   Read the description and understand the challenge ❌.
   Check all the files for the flag ✅ .

   Welp for the intended way, you need to analyze the picture folder, since that is what been told in the description. 

   ![Step1](images/4.1.png)

   Here we can see alot of images, so just extract the images by right clicking it and press export files. Then go to your kali or use online exiftool and analyze the image. In the giraffe image, I placed a comment that saying "The final flag is hidden in the folder: program files/deep_hidden/secrets".

   ![Step2](images/4.2.png)

   So just go there and get the flag.

   ![Step3](images/4.3.png)

   Over here the flag is in some kind of encrypted form (base64), just go to [dcode](https://dcode.fr/en) and repeat the same process and get the flag. 

   FLAG = CyberX{C0ngr4tul4t10ns_0n_f1nd1ng_m3!}

   That is all for the Forensic Odyssey Challenges. 
### 5. ZipCrack 1: The Hidden Lock
   Description: A file waits, sealed tight, its contents hidden behind a lock. The key is somewhere, though it’s not obvious. The path to uncover it lies in persistence, and time is ticking. Will you find the way in?

   Looks like we got a password protected zip file. **Key is somewhere**,while this could mean many things, the most probable one would be that the key is leaked somewhere like in rockyou.txt (A famous wordlist containing a lot of password). JohnTheRipper would use this wordlist to crack the files. 
   
   Now let's see how we can use John to crack this zip file. [JohnTheRipper](https://en.wikipedia.org/wiki/John_the_Ripper).

   First step is changing the zip file into a hash file (cannot skip since John will crack the hash to get the password or something like that 🤓) [Learn more here](https://www.freecodecamp.org/news/crack-passwords-using-john-the-ripper-pentesting-tutorial/)

   So in Kali linux, open your folder where you put the zip files, then open your terminal in that folder. Then change the zip file into hash file by entering this command in your terminal. 

   ```bash
   zip2john <zipfile name @ zipfile path> > <anyname.txt>

   zip2john flag.zip > flag.txt
   ```
   Now you will have the hash, next just use John to get the password

   ```bash
   john <anyname.txt>

   john flag.txt
  ```

  After John successfully cracked the zip file, it will say no password hashes left to crack.

  Next to see the password.

  ```bash
  john --show <anyname.txt>

  john --show flag.txt
  ```  

  The passowrd for out zip file is ```rainbow1```.

  Now use 7z to extract the zip and use the password when prompted.

  ![Step1](images/zip1.1.png)

  Then cd into the folder and cat the flag.

  ![Step2](images/zip1.2.png)

  FLAG : CyberX{J0hn_th3_g04t}

### 6. ZipCrack 2: The Champion Lock
 Description: Another ZIP file blocks your path, but this one carries a hint. The hacker’s obsession with League of Legends may have influenced the password. Look closely—perhaps the password is tied to something familiar to any LoL player.

 Alright this also seems like the same password protected zip file, but this time something is different. **password is tied to something familiar to any LoL player**, this could mean a lot of things like maybe the proffession players or even the character names. Welp we can just do the same steps as above and get the password right?? Welp maybe, I didn't try it 💀. 
 So what to do now? We can't be thinking of bruteforcing 80+ characters and god know how many proffesional players name right? right??

 Take a deep breath and analyze back how John works, he crack/guess the password hash with a list of hash he already has. So how about if we give him a custom word list to crack?? Well that is the intended way to solve this chall, but writing all the character and player name on your own is hard, if you even think of writing it better just test it with the zip file right? So we turn to our best friend, CHATGPT 🐐. We ask him to create a wordlist for us. 

 ```bash
Aatrox
Ahri
Akali
Akshan
Alistar
Amumu
Anivia
Annie
Aphelios
Ashe
Aurelion Sol
Azir
Bard
Bel'Veth
Blitzcrank
Brand
Braum
Caitlyn
Camille
Cassiopeia
Cho'Gath
Corki
Darius
Diana
Dr. Mundo
Draven
Ekko
Elise
Evelynn
Ezreal
Fiddlesticks
Fiora
Fizz
Galio
Gangplank
Garen
Gnar
Gragas
Graves
Gwen
Hecarim
Heimerdinger
Illaoi
Irelia
Ivern
Janna
Jarvan IV
Jax
Jayce
Jhin
Jinx
Kai'Sa
Kalista
Karma
Karthus
Kassadin
Katarina
Kayle
Kayn
Kennen
Kha'Zix
Kindred
Kled
Kog'Maw
KSante
LeBlanc
Lee Sin
Leona
Lillia
Lissandra
Lucian
Lulu
Lux
Malphite
Malzahar
Maokai
Master Yi
Milio
Miss Fortune
Mordekaiser
Morgana
Naafiri
Nami
Nasus
Nautilus
Neeko
Nidalee
Nilah
Nocturne
Nunu & Willump
Olaf
Orianna
Ornn
Pantheon
Poppy
Pyke
Qiyana
Quinn
Rakan
Rammus
Rek'Sai
Rell
Renata Glasc
Renekton
Rengar
Riven
Rumble
Ryze
Samira
Sejuani
Senna
Seraphine
Sett
Shaco
Shen
Shyvana
Singed
Sion
Sivir
Skarner
Sona
Soraka
Swain
Sylas
Syndra
Tahm Kench
Taliyah
Talon
Taric
Teemo
Thresh
Tristana
Trundle
Tryndamere
Twisted Fate
Twitch
Udyr
Urgot
Varus
Vayne
Veigar
Vel'Koz
Vex
Vi
Viego
Viktor
Vladimir
Volibear
Warwick
Wukong
Xayah
Xerath
Xin Zhao
Yasuo
Yone
Yorick
Yuumi
Zac
Zed
Zeri
Ziggs
Zilean
Zoe
Zyra
K'Sante
Milio
Naafiri
Briar
Faker
Caps
Chovy
Nuguri
TheShy
Zeus
Canyon
Jankos
Peanut
Uzi
Gumayusi
Ruler
Mata
Keria
Ming

```

So this is the wordlist i got after prompting the 🐐 GPT, so save this as any file name in the same folder with your zip file for ease, otherwise you need to specify the directory and all. Now change the zip file to hash and feed john this juicy wordlist and let him do the work. 

![Step1](images/2.1.png)

We could also see that the password is ```tryndamere```. Now just get the flag.

![Step2](images/2.2.png)

FLAG: CyberX{pl4se_d0nt_t3ll_m3_y0u_tri3d_th3m_0n3_by_0n3}

### 7. Hex1: The Misleading File

Description: A file has appeared in your path, but something about it doesn't feel right. It’s not what it seems, and the details are hiding in plain sight. Your task: uncover its true identity.

Alright this challenge is pretty straight forward, **uncover its true identity** means just change it's extension. If you open this file in [HexEd](https://hexed.it) or any of your favourite Hex Editor, you will notice that everything looks perfect and let's be forreal, this is forensic, I can't be giving exe file for you to RE right??. You still need to open it in hex editor so that you can get the correct extension which is jpg.

Uninteded solution: Exiftool the file to get the flag since I made the challenge in Canva and somehow the first string I entered is saved in the metadata alongside my full name and matric number 💀. That is why you see the flag in all the Hex Challenges since I just reused the same pictures. 

![Step1](images/hex1.jpg)

FLAG: CyberX{34SY_R1GHT}

### 8. Hex2: The Hidden Code

Description: Files carry secrets, sometimes more than we expect. There’s something in the structure you haven’t quite noticed yet. Look closer, and the truth might reveal itself.

Alright, so we got a jpg file, but cannot open it, and the chall name is Hex, so the only sensible thing to think is that, the magic bytes has been messed up. So load it in [HexEd](https://hexed.it) and observe it's magic bytes.

![Step1](images/hex2,1.png)

So we can see that the magic bytes are messed up but it still has JFIF, which belongs to jpg so, the extension is correct in this file. Now go to [Magic Byte Library](https://en.wikipedia.org/wiki/List_of_file_signatures) and get the jpg magic bytes. ```FF D8 FF E0``` is the mafic byte, now just replace them with the ```AA AA AA AA ``` in the file. 

![Step2](images/HEX2.2.png)

Now save the file and get the flag.

![Step3](images/hex2.jpg)

FLAG: CyberX{3t1ll_34sy}

### 9.  Hex3: The Deceiver’s Trick

Description: Not everything is as it appears. Some things have been altered—perhaps to mislead you. Follow the trail, and the real nature of this file might emerge if you know where to look.

So we got a docx file huh, what's next? a no extension file?, interesting, well looking at the pattern just insert it into the hex editor and see how it goes. 

![Step1](images/hex3.1.png)

Hmmm so we have ```AA AA AA AA``` again, but if you look close enough, we also have  ```IHDR```  which could mean something. When in confusion, ask CHATGPT 🐐. It told me that this is a png file and in GPT we trust. So change the ```AA AA AA AA``` to png magic byte ```89 50 4E 47``` and change the extension to png and see how it goes. 

![Step2](images/hex3.2.png)

Voila we got the flag.

![Step1](images/hex3.png)

FLAG:CyberX{34s13st_h3x}

### 10. Hex4: The Final Fix

Description: Things are not always what they seem. Everything about this file seems a bit off—could it be intentional? The pieces are scattered, but only by restoring them will the hidden truth come to light.
Hint: What you see is not the full story, expand your view. 

Well now it is a file with no extension ha? GG.... Welp let just put it [HexEd](https://hexed.it) and see how it goes.. 

![Step1](images/hex4.1.png)

So it is the same png hile huh? Because of the ```IHDR``` (if it is ```JFIF``` it is then jpg). So let's fix the file and see what happens. Change the ```AA AA AA AA``` to png magic byte ```89 50 4E 47``` and change the extension to png.

![Step2](images/hex4.2.png)

Alright so we got the photo but where is the flag?? It you check the metadata it is the same stupid first flag.... Where is the flag now??. Oh great time for a hint, **not full story, expand your view**, bro who is giving this ass hints... Well nothing can be done, so let's ask 🐐GPT what it thinks. Hmm GPT is giving ass answers so let him rest now and use our brains. There is a slight difference in the picture when compared to the others, somehow it feels *small*. Ohhhhhh so that is what the author meant by expand your view, expand the picture!!! Damn the author is a genius (Self-glaze is crazy bro). 

![Step3](images/hex4.3.png)

Now let surf the internet for any tips, I used resize image in hex editor. Voila found a nice [website explaining this](https://cyberhacktics.com/hiding-information-by-changing-an-images-height/). Sadly he talking about jpg, so we search again and ofc we got the solution from [StackOverflow](https://stackoverflow.com/questions/30550346/understanding-image-its-hex-values). So we play around with the second line..🥸🥸

After a few trial, I did this and got the flag. 

![Step4](images/hex4.4.png)

![Step5](images/hex4.5.png)

FLAG: CyberX{34s13st_h3x}

Truly the easiest hex frr!
### 11. ChronoPuzzle

Description: The hacker left behind four identical images, but they don’t look as innocent as they seem. Hidden in their metadata are fragments of a mysterious code. Arrange them in the correct order by deciphering their timestamps.
flag format = CyberX{string1_string2_string3_string4}

Hmmm 4 cute cat photos named in a order, suspicious.. Well lets try exiftool and see the output. 

![Step1](images/c1.1.png)

Ohh we have a comment in the metadata, so that is the string said in the question huh. Alright let's try the strings accroding to the name then ❌❌❌ ofc it is wrong, it cannot be that simple right?? Lets try analysing the metadata more, since that is what we have been asked in the question. Ohhhhh all the files has a bit similar date/time. Wait, the challenge name is Chrono, chrono means **relating to time**, so that is how we should order the strings huh. So cat->cat4->cat2->cat3!!!

FLAG: CyberX{XJVTQR_PAKZLW_NMTRXF_ZGYCWD}
### 12. Apocalypse
Too lazy to do writeup.....
    
## OSINT
### 1. Rat in the kitchen 1
Description: Rats in the kitchen - it seems like mario brother was arrested while he was eating. What was he eating, in which establishment he was eating and what city was he in when got arrested. 
Flag format :  CyberX{foodname_establishment_city}
Example : CyberX{nasilemak_pizzahut_skudai}

Mario brother? Luigi... when he got arrested m8? Well let's just search Google. Got this [website](https://edition.cnn.com/2024/12/11/us/luigi-mangione-unitedhealthcare-arrest-explained/index.html)

FLAG: CyberX{hashbrown_mcdonald's_altoona}
### 2. Rat in the kitchen 2

Description: Mamma mia, it seems like he was snitched by a employee. Now figure out the alleged snitch. 
Flag format: CyberX{name}
Example: CyberX{mark_zuckerberg}

Well another google search ig... Damn this is boring... 

![Step1](images/mario.png)

Lol first result.

FLAG: CyberX{nancy_parker}
### 3. Outing With Persaka UTM 1

![chall](images/chall1.jpg)

Description: I wonder where this place is?? Flag Format: CyberX{KLCC}

Mate are you showing us the trash dump or satelite kinda thing, anyways there are two ways to solve this, image search (you gonna cry) or stalk Persaka UTM since this is their event. If you choose the former, do tell me how you get, if you use latter, just go to their facebook or insta and stalk them to death. 

![chall](images/persaka.png)

Got this from FB. Since they format used the abbreviation let's try CCoE like what said in the picture and not CCOE

FLAG: CyberX{CCoE}

### 4. Outing With Persaka UTM 2

![chall](images/chall2.jpg)

Desription: After going to the place in the first part, i almost got lost in this jungle in mid of town. Flag format: CyberX{midvalleysouthkey}

Well this can use reverse image I think. But that also no need la bro. Just look at the picture, got ```ORION CLINIC```, search that and you will get the place, Tamarind Square.

FLAG: CyberX{tamarindsquare}
### 5. Outing With Persaka UTM 3

![chall](images/chall3.jpg)

Description: Damn even the toilet in this building is nice, Flag Format: CyberX{Kfc}, only need company name

Nice toilet no cap, got the answer before from the FB post, that must be Dell since they only went to 2 places.

FLAG: CyberX{Dell}

## Misc
### 1. Lucy Relative, Alice

Description: You know lucy right? From the movie... it seems like her relative Alice is currently in a pc belonging to CyberX. You need to figure out what she is doing inside the pc!

Hmmm a video with flickering screens... it might be morse code, but she is inside a pc so maybe the language of computers, binary? Well it is binary and here is the script I used to get the binary.

```python 
import cv2
import numpy as np
from collections import defaultdict

def select_roi(frame):
    """
    Allow user to select the ROI using a GUI
    """
    print("Select the monitor screen region:")
    print("1. Click and drag to select the area")
    print("2. Press ENTER to confirm selection")
    print("3. Press 'c' to cancel and reselect")
    
    roi = cv2.selectROI("Select Monitor Region", frame, fromCenter=False, showCrosshair=True)
    cv2.destroyWindow("Select Monitor Region")
    
    return roi

def analyze_monitor_state(video_path):
    """
    Analyze video frames by second to detect monitor screen state (white=1, black=0)
    Including zero second
    """
    cap = cv2.VideoCapture(video_path)
    
    fps = int(cap.get(cv2.CAP_PROP_FPS))
    print(f"Video FPS: {fps}")
    
    ret, first_frame = cap.read()
    if not ret:
        print("Error reading video")
        return {}
    
    roi = select_roi(first_frame)
    x, y, w, h = map(int, roi)
    
    # Analyze first frame separately for zero second
    roi_area = first_frame[y:y+h, x:x+w]
    gray = cv2.cvtColor(roi_area, cv2.COLOR_BGR2GRAY)
    avg_brightness = np.mean(gray)
    initial_state = 1 if avg_brightness > 128 else 0
    
    # Initialize states with zero second
    states_by_second = defaultdict(list)
    states_by_second[0].append(initial_state)
    
    # Reset to start of video
    cap.set(cv2.CAP_PROP_POS_FRAMES, 0)
    
    frame_count = 0
    
    while cap.isOpened():
        ret, frame = cap.read()
        if not ret:
            break
            
        # Calculate current second
        current_second = int(frame_count / fps)
        
        # Extract and analyze ROI
        roi_area = frame[y:y+h, x:x+w]
        gray = cv2.cvtColor(roi_area, cv2.COLOR_BGR2GRAY)
        avg_brightness = np.mean(gray)
        state = 1 if avg_brightness > 128 else 0
        
        states_by_second[current_second].append(state)
        
        # Display the frame with ROI rectangle and info
        cv2.rectangle(frame, (x, y), (x+w, y+h), (0, 255, 0), 2)
        cv2.putText(frame, f"Second: {current_second}", (x, y-70),
                   cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)
        cv2.putText(frame, f"State: {state}", (x, y-40),
                   cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)
        cv2.putText(frame, f"Brightness: {avg_brightness:.1f}", (x, y-10),
                   cv2.FONT_HERSHEY_SIMPLEX, 0.9, (0, 255, 0), 2)
        
        cv2.imshow('Analysis', frame)
        
        frame_count += 1
        
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break
    
    cap.release()
    cv2.destroyAllWindows()
    
    # Process results by second
    final_states = {}
    for second, states in states_by_second.items():
        average_state = sum(states) / len(states)
        final_states[second] = 1 if average_state > 0.5 else 0
    
    return final_states

def save_binary_sequence(states, output_file):
    """
    Save binary sequence to a text file, ensuring zero second is included
    """
    max_second = max(states.keys())
    # Ensure we start from second 0
    binary_sequence = ''.join(str(states.get(i, 0)) for i in range(max_second + 1))
    
    with open(output_file, 'w') as f:
        f.write(binary_sequence)
    
    print(f"Binary sequence saved to {output_file}")
    print(f"Binary sequence: {binary_sequence}")

def main():
    video_path = 'path to the video'
    output_file = 'binary_sequence.txt'
    
    states_by_second = analyze_monitor_state(video_path)
    
    # Save to file
    save_binary_sequence(states_by_second, output_file)
    
    # Print summary
    total_seconds = len(states_by_second)
    white_seconds = sum(1 for state in states_by_second.values() if state == 1)
    black_seconds = total_seconds - white_seconds
    
    print(f"\nSummary:")
    print(f"Total seconds analyzed: {total_seconds}")
    print(f"Seconds with white screen: {white_seconds}")
    print(f"Seconds with black screen: {black_seconds}")
    print(f"White screen percentage: {(white_seconds/total_seconds)*100:.1f}%")

if __name__ == "__main__":
    main()
```

Run this python code in your kali, remember to set the path to the video. 

![Step1](images/al1.png)

Then don't forget to choose the screen and press enter.

![Step2](images/al2.png)

Voila, you will get this after the analysis is done

![Step3](images/al3.png)

```binary
010000110111100101100010011001010111001001011000011110110100001000110001011011100011010001110010011110010101111100110001011100110101111101100110011101010110111001111101
```

Go to [dcode](https://dcode.fr/en) or [cybcerchef](https://gchq.github.io/CyberChef/) and decode this, I prefer cyberchef, since we know that this is binary.

![Step3](images/al4.png)


That is all the challenges from me. See you guys again 🎊🎊🎊🎊

