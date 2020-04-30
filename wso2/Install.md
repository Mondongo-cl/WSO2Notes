# Installation notes

## TIme Issues

Ensure time format is United States '(yyyy-MM-dd)'


## Certificated Issues

to add a new certificate needs export from browser and import in the keystore  ´\wso2am-3.0.0\repository\resources\security\client-truststore.jks´ the command to import the certificate is

```keytool -import -alias <<your_alias>> -file <<exported_cert_path.cer>> -keystore \wso2am-3.0.0\repository\resources\security\client-truststore.jks -sotepass wso2carbon```

## IP Issues

to set IPV4 as default stack needs to add to the file ´C:\wso2\wso2am-3.0.0\bin\wso2server.bat´ the value ´-Djava.net.preferIPv4Stack=true ´ in the _*CMD_LINE_ARGS*_ variable