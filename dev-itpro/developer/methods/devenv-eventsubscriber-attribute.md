---
title: "EventSubscriber Attribute"
ms.custom: na
ms.date: 10/01/2018
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.service: "dynamics365-business-central"
author: SusanneWindfeldPedersen
---

# EventSubscriber Attribute
Specifies the method to be integration type event subscriber.

## Syntax  
  
```  
[EventSubscriber(ObjectType::ObjectType, ObjectId, 'OnSomeEvent', 'ElementName', SkipOnMissingLicense, SkipOnMissingPermission)]
```    
  
#### Arguments  
*ObjectType*  
Type: Enumeration  
  
Specifies the type of object that publishes the event to subscribe to. The value will depend on the type of event: business, integration, and trigger. 

Business and integration events are published by event publisher methods in objects such as codeunits, pages, or tables. To subscribe to a business or integration type event, you specify the object that contains the event publisher method that defines the event. 

Trigger events are system events that are automatically declared and published in tables and pages. To subscribe to a trigger event, you specify the table or page that published the trigger event.

*ObjectId*  
Type: Integer  

Specifies the ID of the object that that publishes the event to subscribe to.

*OnSomeEvent*  
Type: Text  

Specifies the name of method that publishes the event in the object that is specified by the *ObjectId* parameter. 

*ElementName*  
Type: Text

Specifies the table field that the trigger event pertains to. This argument only requires a value for database trigger events, that is, when the *ObjectType* is set to **table** and the *OnSomeEvent* argument is a validate trigger event, such as `OnAfterValidateEvent`.

*SkipOnMissingLicense*  
Type: Boolean

Specifies what happens to the event subscriber method call when the [!INCLUDE[d365fin_long_md](../includes/d365fin_long_md.md)] license of the user account that is running the current session does not include the codeunit that contains the subscriber method.

**True** will ignore the method call, and the code execution will continue to the next subscriber; **false** will throw an error and the code execution stops. 

*SkipOnMissingPermission*  
Type: Boolean

Specifies what happens to the subscriber method call when the user account that is running the current session does not have permission to the codeunit that contains the event subscriber method. The permissions are defined by the permission sets on the user account in [!INCLUDE[d365fin_long_md](../includes/d365fin_long_md.md)].

**True** will ignore the method call, and the code execution will continue to the next subscriber; **false** will throw an error and the code execution stops. **False** is the default value.

## Example
This example publishes an integration type event by using the OnAddressLineChanged method. The method takes a single text data type parameter. The IncludeSender and GlobalVarAccess arguments are set to **false**.

```
codeunit 50105 MyEventPublisher
{
    [IntegrationEvent(false, false)]
    procedure OnAddressLineChanged(line : Text[100]);
    begin
    end;
}

codeunit 50106 MyEventSubscriber
{
    [EventSubscriber(ObjectType::Codeunit, Codeunit::MyEventPublisher, 'OnAddressLineChanged', '', true, true)]
    local procedure MyProcedure(line: Text[100])
    begin
    end;
}
``` 

## See Also  
 [Events in AL](../devenv-events-in-al.md)  
 [Publishing Events](../devenv-publishing-events.md)   
 [Raising Events](../devenv-raising-events.md)   
 [Subscribing to Events](../devenv-subscribing-to-events.md)   
[Method Attributes](devenv-method-attributes.md)