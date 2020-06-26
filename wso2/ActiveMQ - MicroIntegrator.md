## Add new message into queue

### Notes

#### Insert a number of messages into a queue

```
activemq producer 
--message "<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\"><soapenv:Header/><soapenv:Body><m0:placeOrder xmlns:m0=\"http://services.samples\"><m0:order><m0:price>172.23182849731984</m0:price><m0:quantity>18398</m0:quantity><m0:symbol>IBM</m0:symbol></m0:order></m0:placeOrder></soapenv:Body></soapenv:Envelope>" 
--destination queue://Queue1 
--messageCount 1000
```

#### Enable ActiveMQ serializers

to allow to WSO2 Message processor mediator read messages from activeMQ message store, the microintegrator runtime needs to add the ```-Dorg.apache.activemq.SERIALIZABLE_PACKAGES="*" ``` parameter to the start options of the server runtime.
