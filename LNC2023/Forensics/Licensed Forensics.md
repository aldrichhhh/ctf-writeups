![LicensedForensics1](https://user-images.githubusercontent.com/84762311/233945176-dae2755a-b4cc-4546-8b7b-adc2816d2466.png)


## Description

>We have a rogue forensics investigator who got away with our files and documents! Fortunately, they were not able to destory all evidence before their escape from the compound. We have confiscated his computer and created an image of one of his drives. It is up to you to figure out what he is hiding.
>
>GDrive Link: [https://drive.google.com/file/d/12dN8gxb653xAJsEzXQp3eZMXxIWkhMjI/view?usp=sharing](https://drive.google.com/file/d/12dN8gxb653xAJsEzXQp3eZMXxIWkhMjI/view?usp=sharing)
>
>p.s. Please be careful and do not unintentially change your main system settings.



## Solution

Open up the file with Autopsy and in vol5 > Desktop, I noticed a zip file Secret_Documents.zip. The zip file contains a series of files.

![LicensedForensics2](https://user-images.githubusercontent.com/84762311/233950103-b94b5d97-7b44-4b56-806f-3cf6b593c9cf.png)

The Note.txt contains part of the password for flag.zip. The file also states that the virtual machine license key is the key to flag.zip

![LicensedForensics3](https://user-images.githubusercontent.com/84762311/233951463-04412803-d9d7-445a-b606-42f3b2cfe15e.png)


I then extracted out the flag.zip file by right clicking the file > Extract File(s)

![LicensedForensics9](https://user-images.githubusercontent.com/84762311/233957192-888f284e-8b6d-4154-8858-4b298ef77598.png)


Doing a quick google search, the license key is stored in Computer > HKEY_LOCAL_MACHINE > SOFTWARE > Wow6432Node > VMware, Inc. > VMware Workstation > License.ws.x.x > Serial

![LicensedForensics4](https://user-images.githubusercontent.com/84762311/233952009-f81222b2-8b42-456c-9ada-bbece4c43f82.png)


Using Autopsy's Keyword Search, I search for "Wow6432Node"

![LicensedForensics5](https://user-images.githubusercontent.com/84762311/233955393-28649cab-68f4-47cc-b22d-516272525d73.png)


From the results, one thing that stands out to me is the SOFTWARE-slack.

![LicensedForensics6](https://user-images.githubusercontent.com/84762311/233955465-c412a9ca-b395-4a24-be47-25f3e0005033.png)


Upon further inspection, I am able to find a pastebin link from where the serial number is supposed to be.

![LicensedForensics7](https://user-images.githubusercontent.com/84762311/233956040-cd0c542c-8465-4e42-98e5-420c9748bafd.png)


Navigating to the pastebin, reveals the remaining digits which forms the password "3298394326895379123"

![LicensedForensics8](https://user-images.githubusercontent.com/84762311/233956490-4b1f98f6-3d95-4b65-9353-f94e18e7edd0.png)


Unzipping flag.zip with the password gives a flag.pdf which contains the flag

![LicensedForensics10](https://user-images.githubusercontent.com/84762311/233958102-09e5ee3a-fb52-4827-bd90-e30220aa6105.png)




## Flag

LNC2023{ou7of51ght_outofm1nd}