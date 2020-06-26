## Add new message into queue

### Notes

folow [this](/wso2/Install.md&_a=preview&anchor=setting-up-the-micro-integrator-with-activemq%C2%B6) link.

To insert a number of messages into a queue

```
activemq producer 
--message "<soapenv:Envelope xmlns:soapenv=\"http://schemas.xmlsoap.org/soap/envelope/\"><soapenv:Header/><soapenv:Body><m0:placeOrder xmlns:m0=\"http://services.samples\"><m0:order><m0:price>172.23182849731984</m0:price><m0:quantity>18398</m0:quantity><m0:symbol>IBM</m0:symbol></m0:order></m0:placeOrder></soapenv:Body></soapenv:Envelope>" 
--destination queue://Queue1 
--messageCount 1000```


