# Installation notes

## TIme Issues

Ensure time format is United States '(yyyy-MM-dd)'


## Certificated Issues

to add a new certificate needs export from browser and import in the keystore  ´\wso2am-3.0.0\repository\resources\security\client-truststore.jks´ the command to import the certificate is

```keytool -import -alias <<your_alias>> -file <<exported_cert_path.cer>> -keystore \wso2am-3.0.0\repository\resources\security\client-truststore.jks -sotepass wso2carbon```

## IP Issues

to set IPV4 as default stack needs to add to the file ´C:\wso2\wso2am-3.0.0\bin\wso2server.bat´ the value ´-Djava.net.preferIPv4Stack=true ´ in the _*CMD_LINE_ARGS*_ variable

## Change Password Tools
 
Install ant tool 1.8 runtime conpatible by example 1.0.7, don't forget define ```ANT_HOME``` and add the ```%ANT_HOME%\Bin``` to ```Path```

## Dash Board Issues

Version 3.0.0 not works with chrome in my tests, I use brave to see the information, one the dashboards is loaded the dashboard process thow a exception look like normar, and well-know bug.


```keytool -export -alias wso2carbon  -file wso2carbon_back.cer -keystore \wso2am-3.0.0\repository\resources\security\wso2carbon.jks -storepass wso2carbon```

```keytool -delete -alias wso2carbon  -keystore \wso2am-3.0.0\repository\resources\security\client-truststore.jks -storepass wso2carbon```

```keytool -import -alias wso2carbon  -file wso2carbon_back.cer -keystore \wso2am-3.0.0\repository\resources\security\client-truststore.jks -sotepass wso2carbon```
