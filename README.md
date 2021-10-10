# DomIs
DomIs pentest training write up.


```
Starting with Nmap scan :
```
![alt text](https://user-images.githubusercontent.com/61753065/136694309-a759ea5a-429b-4f2a-8fbb-e466494966f4.png)

```
An account is leaked in the Web pag : 
```
![alt text](https://user-images.githubusercontent.com/61753065/136694322-d5e5b980-d1f9-4371-8075-6f620ee16a82.png)

```
Find the account password by using hydra on SMB:
```
![alt text](https://user-images.githubusercontent.com/61753065/136694370-5e204c9b-ac3c-4d78-a930-db70893608b0.png)

```
Then we can access the shared folder « HR »:
```
![alt text](https://user-images.githubusercontent.com/61753065/136694377-3edfc3c6-227e-4c38-8f46-6109a3df2706.png)

```
We can find a keepass database in the « save » folder. Get this DB and try to brut it with john:
```
![alt text](https://user-images.githubusercontent.com/61753065/136694391-647b17c4-92ff-4671-bf10-ab5795484a8c.png)
![alt text](https://user-images.githubusercontent.com/61753065/136694399-c04bb655-3ef8-4bf2-8b77-fcd1d44f0696.png)

```
Now lets open this keepass database using KeePassXC :

First, its an old keepass database, we have to use the « import » option in keepassXC.
Secondly, save the updated DB.
Finaly, get the « support » account stored in the DB and the K4 flag :
```
![alt text](https://user-images.githubusercontent.com/61753065/136694410-9f785f77-1b95-4d1f-add7-41ed94ac6a7e.png)

```
Using the new account on SMB again and get access to « SI » shared folder:
```
![alt text](https://user-images.githubusercontent.com/61753065/136694441-333045b1-2d10-473f-9dc8-296a21139bef.png)

```
We can get 2 files « log.au3 » and « log.exe ».
```
![alt text](https://user-images.githubusercontent.com/61753065/136694451-579352f0-b7ec-4114-a31e-999bb3c6f6fe.png)

```
au3 is an extension used for AutoIT files, the .exe must contain the LOGIN and PASSWORD of the account used to launch the .bat script (OFC the admin account).

We can decompil this file IF the script was compiled with an old version of AutoIT by using a tool named « Exe2Aut ». We can found that tool directly in the AutoIT (old version) installation folder in « \extra ». 

SO ! We need a WindowsBox and an old AutoIT version (version 3.2.0.1’s OK) :
```
https://www.autoitscript.com/autoit3/files/archive/autoit/

```
Get the EXE file in your WindowsBox and decompil him :
```
![alt text](https://user-images.githubusercontent.com/61753065/136694465-d9839ab6-3017-4039-808d-b8bc4567a199.png)

```
You can now, read the script in clear text and the « pil_flag » !
```
![alt text](https://user-images.githubusercontent.com/61753065/136694506-d5a322bd-3b38-42a5-ad2d-9b04ecc42065.png)

```
Lets get a shell by using wmiexec and take the admin flag :
```
![alt text](https://user-images.githubusercontent.com/61753065/136694523-d559af81-e85d-4f13-a2b2-55bcb7792d2a.png)

```
And get the admin_flag in the « administrateur » desktop folder :
```
![alt text](https://user-images.githubusercontent.com/61753065/136694558-82d73462-64de-4820-9011-4af426e9aea6.png)

```
Finaly, dump the « anonymous » hashed password and get the final answer :
```
![alt text](https://user-images.githubusercontent.com/61753065/136694583-6827410e-cfb9-4709-ab06-2fce512edd1f.png)
