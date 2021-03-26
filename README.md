# Dealing with SSL Authentication on a secure Corporate Network

[Credits](https://medium.com/@iffi33/dealing-with-ssl-authentication-on-a-secure-corporate-network-pip-conda-git-npm-yarn-bower-73e5b93fd4b2)

If you are working with secure corporate proxy network most of the time you have to deal with some SSL authentication issues while installing packages, downloading files using wget, curl, python, nodejs from command line which you can easily do from your browser. To deal with these issues sometimes you have to go around different approaches or disable SSL verification (unsafe) and for different technologies there are different ways to configure these options.

NOTE:
---
For Insecure communication you can use the commands / parameters metioned in this file to disable SSL verification. However, remember that you still might get warnings and also it is insecure.


For the secure communication using SSL over a secure network you would be needing a digitally signed certificate file to configure for different services and software.
If you already have a certificate available from your corporate network you should download that certificate using your browser to your Downloads folder. And create a .certificate directory is user profile folder.
```
mkdir %USERPROFILE%\.certificates
mkdir C:\Users\youruser\.certificates
```
Next move the downloaded certificate to the .certificates directory
```
copy %USERPROFILE%\Downloads\yourcertname.crt\ %USERPROFILE%\.certificates\
```

Either you have link provided from your network for certificate or use this step by step guide to download from browser.

[Installing the SSL Certificate through a Web Browser](https://support.globalsign.com/customer/en/portal/articles/1211541-install-client-digital-certificate---windows-using-chrome)

For Chrome go to Settings -> Advanced Settings -> HTTPS / SSL

## **GIT**
---
Disabling SSL ( unsafe not recommended)
```
git config http.sslVerify false
```
Configuring certificate while SSL authentication is true (recommended)
```
git config --global http.sslverify true
git config --global url.https://.insteadOf git://
git config --global http.sslCAInfo C:\Users\youruser\.certificates\yourcertname.crt
```


## **YARN**
---
Disabling SSL ( unsafe not recommended)
```
yarn config set strict-ssl false
```
Configuring certificate while SSL authentication is true (recommended)
```
yarn config set strict-ssl true
yarn config set cafile C:\Users\youruser\.certificates\yourcertname.crt
```

## **NPM / Node Package Manager**
---
Disabling SSL ( unsafe not recommended)
```
npm config set strict-ssl false
```
Configuring certificate while SSL authentication is true (recommended)
```
npm config set strict-ssl true
npm config -g set cafile C:\Users\youruser\.certificates\yourcertname.crt
npm install packagename
```

## **PIP / Python Package Manager:**
---
Disabling SSL ( unsafe not recommended)
```
pip install --trusted-host pypi.python.org packagename
```
Configuring certificate while SSL authentication is true (recommended)
```
pip --cert C:\Users\youruser\.certificates\yourcertname.crt install packagename
```

## **AWS-CLI**
---
Disabling SSL ( unsafe not recommended)

Use the --no-verify-ssl parameter with each command

e.g.

```
aws cloudformation deploy --stack-name mystack --template-file mytemplatefile.yaml --no-verify-ssl 
```

## **BOWER**
---
Create a file .bowerrc in your user profile directory

Disabling SSL ( unsafe not recommended). In .bowerrc file add following snippet and save.
```
{ "strict-ssl": false }
```

Configuring certificate while SSL authentication is true (recommended). In .bowerrc file add following snippet and save.
```
{ 
    "strict-ssl": true,
    "ca": "C:\Users\youruser\.certificates\yourcertname.crt"
}
```

## **CONDA**
---
Disabling SSL ( unsafe not recommended)
```
conda config --set ssl_verify False
```
Configuring certificate while SSL authentication is true (recommended)
```
conda config --set ssl_verify True
conda config --set ssl_verify C:\Users\youruser\.certificates\yourcertname.crt
```