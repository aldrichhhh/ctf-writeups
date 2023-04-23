![](https://user-images.githubusercontent.com/84762311/233588550-294f1a40-064d-437a-a3cf-628cfdba8ebb.png)



## Description

>The engineers mind set has been present with us since the start of time, can you restore and repair the files to get the hidden key.

Files: [RestorationRepair.zip](https://github.com/aldrichhhh/Ethical-hacking/files/11294074/RestorationRepair.zip)

## Solution

Static analysis on the Start.JPG file to check any hidden strings in the file. From the result, the first half of the password is given "asd9230dkaos". The result also show that "Second half is required:" which refers to "TgH8U."" Combining them together, we get the password "asd9230dkaosTgH8U" for clue.zip.
![a](https://user-images.githubusercontent.com/84762311/233594253-06d670af-ce81-436c-b2df-ed7c49eaf811.png)

Extracting the clue.zip file, we get Clue.JPG and key.zip
![ResstorationRepair2](https://user-images.githubusercontent.com/84762311/233635039-82ff03cb-1cf3-48bb-ac02-2f2b0a230e71.png?width=10)

Attempting to open the Clue.JPG file returns an error "Not a JPEG file starts with 0x00 0x00". Thus, we have to repair the Start of Image (SOI) segment.
![ResstorationRepair3](https://user-images.githubusercontent.com/84762311/233636395-8d481c0e-cff9-4a4f-afde-d15c37c3852a.png)

![ResstorationRepair4](https://user-images.githubusercontent.com/84762311/233640627-7565cdf8-fc4b-4429-aa37-4556bb358f4f.png)


Reopening the repaired file, it shows part of the password  "8as9Lm0". 
![ResstorationRepair5](https://user-images.githubusercontent.com/84762311/233641153-73bdad82-ab39-4ca1-a30d-04f609607a75.png)



I then printed out the strings in the file and uncovered "2/3 is required 90siwH Mh89 2930p3". However, I tried all possible combination but to no avail.
![ResstorationRepair6](https://user-images.githubusercontent.com/84762311/233641992-6e15f377-0b88-45ba-8053-226d08610d01.png)

Further analysing the strings in a hex dump, I noticed that "p3" is a separate value from "2930" thus I retried with the password "Mh8929308as9Lm0" and it worked.
![ResstorationRepair7](https://user-images.githubusercontent.com/84762311/233643161-9f65d048-57b1-484a-8f6e-7120036925cf.png)

![ResstorationRepair8](https://user-images.githubusercontent.com/84762311/233644822-b27ecd89-456f-4e2d-9182-5bf4dd4d8c8a.png)


## Flag

LNC2023{TgH8UMh898as9Lm0}