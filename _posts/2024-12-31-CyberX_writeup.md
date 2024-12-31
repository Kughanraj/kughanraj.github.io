---
title: CyberX CyberSentinel Writeup By PLLSKY
date: 2024-12-31 00:00:00 +0800
categories: [CTF, Writeup, CyberX]
tags: [ctf, writeup, cyberx, cybersentinels]
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

  ![Step1]()

  Then cd into the folder and cat the flag.

  ![Step2]()

  FLAG : CyberX{J0hn_th3_g04t}

### 6. ZipCrack 2: The Champion Lock
 Description: Another ZIP file blocks your path, but this one carries a hint. The hacker’s obsession with League of Legends may have influenced the password. Look closely—perhaps the password is tied to something familiar to any LoL player.

 Alright this also seems like the same password protected zip file, but this time something is different. **password is tied to something familiar to any LoL player**, this could mean a lot of things like maybe the proffession players or even the character names. Welp we can just do the same steps as above and get the password right?? Welp maybe, I didn't try it 💀. 
 So what to do now? We can't be thinking of bruteforcing 80+ characters and god know how many proffesional players name right? right??

 Take a deep breath and analyze back how John works, he crack/guess the password hash with a list of hash he already has. So how about if we give him a custom word list to crack?? Well that is the intended way to solve this chall, but writing all the character and player name on your own is hard, if you even think of writing it better just test it with the zip file right? So we turn to our best friend, CHATGPT 🐐. We ask him to create a wordlist for us. 

 ```txt
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

So this is the wordlist i got after prompting the 🐐 GPT, so save this as any file name in the same folder with your zip file for ease, otherwise you need to specify the directory and all. So 

### 7. Hex1: The Misleading File
### 8. Hex2: The Hidden Code
### 9.  Hex3: The Deceiver’s Trick
### 10. Hex4: The Final Fix
### 11. ChronoPuzzle
### 12. Apocalypse
    
## OSINT
### 1. Rat in the kitchen 1
### 2. Rat in the kitchen 2
### 3. Outing With Persaka UTM 1
### 4. Outing With Persaka UTM 2
### 5. Outing With Persaka UTM 3

## Misc
### 1. Lucy Relative, Alice

That is all the challenges from me. 

