# owasp-api-lab
A lab focused on protecting vulnerable APIs with Apigee

## The server in question
http://35.228.10.151/

## The rest apis
http://35.228.10.151/rest

## Searching the product api 
http://35.228.10.151/rest/products/search?q=orange

## Some concepts
We'll explore several concepts through a series of ad-hoc labs

### What's the site like?
Crazy insecure. The nightmare site everyone is afraid to leave wide open on the internet

### And what resources need protecting?
This part is interesting with regards to how it relates to APIs?

### What about limiting returns?
Have a look at the json threat protection policy

### How about SQL Injection
Consider the Regulal Expressioni Threat policy.... We'll use something like this:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<RegularExpressionProtection async="false" continueOnError="false" enabled="true" name="RegEx.SQLInjection">
    <DisplayName>RegEx.SQLInjection</DisplayName>
    <QueryParam name="q">
        <Pattern>[\s]*(?i)((delete)|(exec)|(drop\s*table)|(insert)|(shutdown)|(update)|(\bor\b))</Pattern>
    </QueryParam>
</RegularExpressionProtection>
```
### This is great but it feels a bit adhoc

### Hiding ugly errors that give away info
```xml
<AssignMessage name="ReturnGenericError">
  <Set>
    <Payload type="text/plain">SERVICE UNAVAILABLE. PLEASE CONTACT SUPPORT: support@company.com.</Payload>
  </Set>
</AssignMessage>
```

Plus a default fault rule

```xml
<DefaultFaultRule name="fault-rule">
    <Step>
      <Name>ReturnGenericError</Name>
    </Step>
    <AlwaysEnforce>true</AlwaysEnforce>
  </DefaultFaultRule>
```

### Other considerations?
This was really just the tip of the iceberg of course
