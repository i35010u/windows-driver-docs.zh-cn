---
title: 设置请求和响应架构
description: 下面是集请求架构和相应的响应架构定义和各自的示例。
ms.assetid: 88E7F06C-3232-48C3-A0D6-2BEFF4ABA188
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9fddf9586613f4a19dc42e81e627951ccef7398
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367591"
---
# <a name="set-request-and-response-schemas"></a>设置请求和响应架构


下面是集请求架构和相应的响应架构定义和各自的示例。

## <a name="set-request-schema"></a>设置请求架构


组请求用于写入打印机属性的值。

在此示例中，请求尝试设置两个属性。 第二个是故意错误： 内存属性不是可写。 对此请求的响应，请参阅下面的设置响应架构。

```xml
<bidi:Set xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.DeviceInfo:Location'>
    <BIDI_STRING>supply room</BIDI_STRING>
  </Query>
  <Query schema='\Printer.Configuration.Memory:Size'>
    <BIDI_INT>4096</BIDI_INT>
  </Query>
</bidi:Set>
```

正式定义的集请求架构

```xml
<?xml version='1.0'?>
<schema targetNamespace="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns ='http://www.w3.org/2001/XMLSchema'>
  <element name='Set'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Query'>
          <complexType>
            <choice>
              <element name='BIDI_STRING' type='string'/>
              <element name='BIDI_TEXT'   type='string'/>
              <element name='BIDI_ENUM'   type='string'/>
              <element name='BIDI_INT'    type='integer'/>
              <element name='BIDI_FLOAT'  type='float'/>
              <element name='BIDI_BOOL'   type='boolean'/>
              <element name='BIDI_BLOB'   type='base64Binary'/>
            </choice>
            <attribute name='schema' type='bidi:SCHEMA_STRING' use='required'/>
            <anyAttribute namespace='##other' processContents='skip'/>
          </complexType>
          </element>
      </sequence>
      <anyAttribute namespace='##other' processContents='skip'/>
    </complexType>
  </element>
  <simpleType name='SCHEMA_STRING'>
    <restriction base='string'>
      <pattern value='\\\w+(\.\w+)*\:\w+'/>
    </restriction>
  </simpleType>
</schema>
```

## <a name="set-response-schema"></a>设置响应架构


这是对上述集请求的响应。 请注意，写入操作成功后，原始查询返回的值是不包含任何值。 如果操作失败，则返回错误代码。

```xml
<bidi:Set xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.DeviceInfo:Location'/>
  <Query schema='\Printer.Configuration.Memory:Size'>
    <Error>ERROR_BIDI_SCHEMA_READ_ONLY</Error>
  </Query>
</bidi:Set>
```

集响应架构中的正式定义

```xml
<?xml version='1.0'?>
<schema targetNamespace="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns ='http://www.w3.org/2001/XMLSchema'>
  <element name='Set'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Query'>
          <complexType>
            <sequence minOccurs='0' maxOccurs='1'>
              <element name='Error' type='integer'/>
            </sequence>
            <attribute name='schema' type='bidi:SCHEMA_STRING' use='required'/>
          </complexType>
        </element>
      </sequence>
    </complexType>
  </element>
  <simpleType name='SCHEMA_STRING'>
    <restriction base='string'>
      <pattern value='\\\w+(\.\w+)*\:\w+'/>
    </restriction>
 </simpleType>
</schema>
```

## <a name="related-topics"></a>相关主题

[双向通信架构](bidirectional-communication-schema.md)  

[SendRecvXMLStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)  
