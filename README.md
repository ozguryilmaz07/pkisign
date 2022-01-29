# PKI_Digital_Signature_PDF_USB_Token

<br>

## Overview
![Group-1198](https://user-images.githubusercontent.com/70335592/125410523-a0c10980-e3c5-11eb-85c3-e99214753fc5.png)

PKI tokens are hardware devices that store digital certificates and private keys securely. When you need to encrypt, decrypt or sign something, the token does this internally in a secure chip meaning the keys are never at risk of being stolen.
 

<br>

USB token based certificates are an implementation of PKCS#11, one of the Public-Key Cryptography Standards. Digital signature certificates are issued by a Certificate Authority (CA).

<br>



## PKCS#11 

The PKCS #11 standard defines a platform-independent API to cryptographic tokens, such as hardware security modules (HSM) and smart cards.
The API defines most commonly used cryptographic object types (RSA keys, X.509 Certificates, DES/Triple DES keys, etc.) and all the functions needed to use,
create/generate, modify and delete those objects [Read more PKCS11]( https://docs.oracle.com/javase/7/docs/technotes/guides/security/p11guide.html#Intro).

<br>

## iText

iText 7 for Java represents the next level of SDKs for developers that want to take advantage of the benefits PDF can bring. 
Equipped with a better document engine, high and low-level programming capabilities and the ability to create, edit and enhance PDF documents, 
iText 7 can be a boon to nearly every workflow. [Read more iText](https://itextpdf.com/en/solutions/electronic-signatures-pdf).

---


<br>
 
 ## Specifications of the USB Token that worked on :

Token name: eToken

Token category: Hardware

Product name: SafeNet eToken 5110 FIPS

Model: Token 15.0.0.3 15.0.19

Card type: Java Card

OS version: eToken Java Applet 1.8.5

---
<br>

 ## installation
 
 <br>
 
 The programs and systems used and the most important uses Software package must be installed :

 ### 1- safeNet Authentication Client

* Change Token PIN
* Change Token Name
* Install tokens drivers
* Insert token PIN when need to Sign or decrypt process


### 2-Entrust Entelligence Security Provider

* Signing & Encryption Files ,Emails
* Certificates Explore
* Check validity of Certificate
* Create Encryption Group
*  Exchange Digital Certificates With others


### 3-Download eTPKCS11.dll
### 4-Download sunpkcs11.jar

### 5 Add Maven pom.xml

 ```
 <dependencies>  
     <dependency>
    	<groupId>com.itextpdf</groupId>
    	<artifactId>itextpdf</artifactId>
    	<version>5.5.9</version>
	</dependency>
	<dependency>
        <groupId>org.bouncycastle</groupId>
        <artifactId>bcprov-jdk15on</artifactId>
        <version>1.49</version>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>org.bouncycastle</groupId>
        <artifactId>bcpkix-jdk15on</artifactId>
        <version>1.49</version>
        <optional>true</optional>
    </dependency>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.8.2</version>
        <scope>test</scope>
    </dependency>   
  </dependencies>
 ```




---
<br>

## Add an external configuration file which content following information:

In order to enable the JDK to access the security token, you will first need to create a configuration file. Open any plain-text editor and create a file named eToken.cfg. The file should contain 2, possibly 3, lines:

* Add the username of the token <br>
* Adding the path of the library dedicated to the usb token, which is the eTPKCS11.dll library <br>
* Add the USB slot


```
name=eTokenn 
library=c:\WINDOWS\system32\eTPKCS11.dll  
slot=0
```

Note: The default slot number when left unspecified is 0. SafeNet eToken 5100 will automatically assign to slot 0, therefore there will be no need for the slot line in the .cfg file. However this may need to be changed depending on the number of eTokens/SmartCard readers installed. The default slot number for the SafeNet Ikey 4000 is slot 3. The slot line will be required when using a SafeNet iKey 4000.

---
<br>

## Also, add an external library, which is sunpkcs11.jar to run  provider PKCS11 :
```
 sun.security.pkcs11.SunPKCS11 providerPKCS11 = new sun.security.pkcs11.SunPKCS11(pkcs11Config);
```


---
<br>

# Run the program
When you run the program, a window will appear to enter the password to be able to connect to the USB Token and get the Certificates
<br>

![PKI23](https://user-images.githubusercontent.com/70335592/126527885-e50af583-0970-4032-ae43-776b42326524.png)

<br>



```
 KeyStore.CallbackHandlerProtection chp = new KeyStore.CallbackHandlerProtection(new MyGuiCallbackHandler() {});
 KeyStore.Builder builder = KeyStore.Builder.newInstance("PKCS11", null, chp);
 KeyStore keyStore = builder.getKeyStore();
 ```
<br>


#### After that, it will select the required certificates, which are the encryption certificate

 ```
  if( x509Certificate.getKeyUsage()[2] == true) 
 ```
 <br>
 
 
 #### and access to the keys
 
 
  ```
 Key key = keyStore.getKey(alias, null); 
 privateKey  =  (PrivateKey )key ; 
 publicKey = x509Certificate.getPublicKey();
  ```
  <br>
  
### Then the program will Digital Sign and create a new file


<br>

![92](https://user-images.githubusercontent.com/70335592/130411412-ac79feb2-2b7b-40cb-99bb-2d8a5713f319.png)

 <br>
 
![94](https://user-images.githubusercontent.com/70335592/130411416-406cc4a4-a138-4082-9481-b2aef1c854e6.png)

 <br>
 
## Signature information

<br>


![97](https://user-images.githubusercontent.com/70335592/130411418-8eb201ce-46f6-42ec-adcd-247640e75b72.png)




---

<br>

### Good Luck <img src="https://media.giphy.com/media/hvRJCLFzcasrR4ia7z/giphy.gif" width="30px"> 
