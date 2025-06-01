---
layout: post
title: CyberX-ISSYemen-CTF
date: 2025-06-01 14:15 +0800
categories: [CTF, Writeup]
tags: [ctf,writeup,cyberx,issyemen]
---

# Welcome to my ISS Yemen x CyberX CTF writeup

This time only 3 forensic(??) challenges from me and all of them are Hex Editing since I was lazy as hell

## Forensic

>The challenges are:

### 1. Can You Fix Me 1 

  Description: 
  Heard you can fix everything.. Try fixing this!

  [Download](https://drive.google.com/file/d/1fSLItXWjdlM5fBKAa-n2nmQwA7fB0CPA/view?usp=drive_link) in case you want to try the chall..

  ![Step1](images/1.1.png)

  Open the file in Hexed or IMHex or any Hex Editor of your preference, i just use [CyberChef](https://gchq.github.io/CyberChef/) 

  You can enter the file as input in CyberChef 

  ![step2](images/1.1.png)

  Here we can see that the magic bytes are messed up, I mean no jpg starts with ```aa aa aa aa```, they start with ```FF D8 FF E0``` 

  So change it and we can also try to render the picture in CyberChef (I love you!!) Just use ```From Hex``` and ```Render Image``` recipes. 

  ![Step3](images/1.1.png)

  This is the picure we get, however there is no flag visible here... If you look hard enough you can see that the picture is not full. I just changed the hex that controls the height.. you can ask chatgpt to explain more about this part.. but normally jpg height hex is stated after ``` FF C0``` however this jpg does not have any of that but chatgpt also said that ``` FF C1 ``` ```FF C2``` are used sometimes and to our luck there exists ```FF C2``` in our jpg.

  ![Step4](images/1.1.png)

  So just play around the bytes and we can see that if we change the ``04`` TO ``05`` we can see the flag.

  ![step5](images/1.1.png)

  FLAG: CyberX{34SY_R1GHT?}


### 2. Can You Fix Me 2

  Description:
  Can you open this file from Hisyam cause I can't open it....

  [Download](https://drive.google.com/file/d/1xvleNMksIE5cO0dxuUIYnVY1bZcMAMEf/view?usp=sharing)

  So this challenge is same as the above, but just one different is there, the are random ```hisyam``` and ```hhisyamisyam``` inside the hexs...
  Just ask chatgpt to make a script for clean this strings...
  Before that make sure to do all the things from the above chall (change magic bytes and the height!)

  This is how the picture looks after fixing the magic byte and height!

  ![Step1](images/1.1.png)
  
  ```python
  # File paths
corrupted_file = 'corrupted.jpg'
cleaned_file = 'cleaned.jpg'

# Patterns to remove
exact = b'hisyam'
trap = b'hhisyamisyam'

# Read corrupted file
with open(corrupted_file, 'rb') as f:
    data = f.read()

# Step 1: Remove bait payloads (longer overlapping version)
data = data.replace(trap, b'')

# Step 2: Remove all exact "hisyam" (in case some were not in a trap)
data = data.replace(exact, b'')

# Save cleaned version
with open(cleaned_file, 'wb') as f:
    f.write(data)

print(f'Removed all exact "hisyam" and trap payloads "hhisyamisyam". Cleaned file saved as {cleaned_file}')
  ``` 

So after cleaning this, you will get this cleaned.jpg

![Step2](images/1.1.png)

FLAG: CyberX{YoU_F1X3D_M3!}






