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

## Add APIM Cert to microgateway


#### Export
```keytool -export -alias wso2carbon -file wso2carbon_bak.cer -keystore C:\wso2\wso2am-3.0.0\repository\resources\security\wso2carbon.jks -storepass wso2carbon```

#### import

```keytool -import -trustcacerts -alias wso2carbon_new -file wso2carbon_bak.cer -keystore ballerinaKeystore.p12 -storepass ballerina```

### Installation Issues Micro Integration Studio

if you are experimenting dificulties to see the artifacts configuration forms.

#### Step 1: add a manifest file to change the IDE display mode.


```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0" xmlns:asmv3="urn:schemas-microsoft-com:asm.v3">
    <description>eclipse</description>
    <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">
        <security>
            <requestedPrivileges>
                <requestedExecutionLevel xmlns:ms_asmv3="urn:schemas-microsoft-com:asm.v3"
                               level="asInvoker"
                               ms_asmv3:uiAccess="false">
                </requestedExecutionLevel>
            </requestedPrivileges>
        </security>
    </trustInfo>
    <asmv3:application>
        <asmv3:windowsSettings xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">
            <ms_windowsSettings:dpiAware xmlns:ms_windowsSettings="http://schemas.microsoft.com/SMI/2005/WindowsSettings">false</ms_windowsSettings:dpiAware>
        </asmv3:windowsSettings>
    </asmv3:application>
</assembly>

```

#### Step 2: Add into window registry a new dword value

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\SideBySide]
"PreferExternalManifest"=dword:00000001

```





this file has to be named as the eclipse executable file, this solution only was tested on windows 10 hi resolutions screens.

by example the name to IntegrationStudio must be ```IntegrationStudio.exe.manifest```

### Setting up the Micro Integrator with ActiveMQ¶
Follow the instructions below to set up and configure.

Download Apache ActiveMQ.
Download and install WSO2 Micro Integrator.
Copy the following client libraries from the ACTIVEMQ_HOME/lib directory to the MI_HOME/lib directory.

#### ActiveMQ 5.8.0 and above

- activemq-broker-5.8.0.jar
- activemq-client-5.8.0.jar
- activemq-kahadb-store-5.8.0.jar
- geronimo-jms_1.1_spec-1.1.1.jar
- geronimo-j2ee-management_1.1_spec-1.0.1.jar
- geronimo-jta_1.0.1B_spec-1.0.1.jar
- hawtbuf-1.9.jar
- Slf4j-api-1.6.6.jar
- activeio-core-3.1.4.jar (available in the ACTIVEMQ_HOME/lib/optional directory)
#### Earlier version of ActiveMQ

- activemq-core-5.5.1.jar
- geronimo-j2ee-management_1.0_spec-1.0.jar
- geronimo-jms_1.1_spec-1.1.1.jar

https://ei.docs.wso2.com/en/latest/micro-integrator/setup/brokers/configure-with-ActiveMQ/

Open the deployment.toml file from the 
- MI_TOOLING_HOME/Contents/Eclipse/runtime/microesb/conf/ (in MacOS) or 
- MI_TOOLING_HOME/runtime/microesb/conf/ (in Windows/Linux)


directory and add the configurations given below. This is required for enabling the broker to store messages.

```
[[transport.jms.listener]]
name = "myTopicListener"
parameter.initial_naming_factory = "org.apache.activemq.jndi.ActiveMQInitialContextFactory"
parameter.provider_url = "tcp://localhost:61616"
parameter.connection_factory_name = "TopicConnectionFactory"
parameter.connection_factory_type = "topic"
parameter.cache_level = "consumer"

[[transport.jms.listener]]
name = "myQueueListener"
parameter.initial_naming_factory = "org.apache.activemq.jndi.ActiveMQInitialContextFactory"
parameter.provider_url = "tcp://localhost:61616"
parameter.connection_factory_name = "QueueConnectionFactory"
parameter.connection_factory_type = "queue"
parameter.cache_level = "consumer"

[[transport.jms.sender]]
name = "myTopicSender"
parameter.initial_naming_factory = "org.apache.activemq.jndi.ActiveMQInitialContextFactory"
parameter.provider_url = "tcp://localhost:61616"
parameter.connection_factory_name = "TopicConnectionFactory"
parameter.connection_factory_type = "topic"
parameter.cache_level = "producer"

[[transport.jms.sender]]
name = "myQueueSender"
parameter.initial_naming_factory = "org.apache.activemq.jndi.ActiveMQInitialContextFactory"
parameter.provider_url = "tcp://localhost:61616"
parameter.connection_factory_name = "QueueConnectionFactory"
parameter.connection_factory_type = "queue"
parameter.cache_level = "producer"
```