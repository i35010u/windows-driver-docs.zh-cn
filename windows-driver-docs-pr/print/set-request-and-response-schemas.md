---
title: 设置请求和响应架构
description: 下面列出了设置请求架构和相应的响应架构定义以及每个定义的示例。
ms.assetid: 88E7F06C-3232-48C3-A0D6-2BEFF4ABA188
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeafe08dcd6617322b6ee5d48662f491b5c18d20
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217432"
---
# <a name="set-request-and-response-schemas"></a>设置请求和响应架构


下面列出了设置请求架构和相应的响应架构定义以及每个定义的示例。

## <a name="set-request-schema"></a>设置请求架构


Set 请求用于将值写入打印机属性。

在此示例中，请求将尝试设置两个属性。 第二个错误是有意的错误：内存属性不可写。 有关此请求的响应，请参阅下面的设置响应架构。

```xml
<bidi:Set xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.DeviceInfo:Location'>
    <BIDI_STRING>supply room</BIDI_STRING>
  </Query>
  <Query schema='\Printer.Configuration.Memory:Size'>
    <BIDI_INT>4096</BIDI_INT>
  </Query>
</bidi:Set>
```

集请求架构的正式定义

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns ='https://www.w3.org/2001/XMLSchema'>
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


这是对上述集请求的响应。 请注意，当写操作成功时，将返回不带任何值的原始查询值。 如果操作失败，则返回错误代码。

```xml
<bidi:Set xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.DeviceInfo:Location'/>
  <Query schema='\Printer.Configuration.Memory:Size'>
    <Error>ERROR_BIDI_SCHEMA_READ_ONLY</Error>
  </Query>
</bidi:Set>
```

设置响应架构的正式定义

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
     xmlns ='https://www.w3.org/2001/XMLSchema'>
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

[SendRecvXMLStream](/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)