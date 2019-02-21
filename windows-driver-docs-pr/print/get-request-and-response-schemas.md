---
title: 获取请求和响应架构
description: 下面是 Get 请求架构和相应的响应架构定义和各自的示例。
ms.assetid: 48980220-4DD6-4785-AAC1-850F8FBE49EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 402649b40d3ff825fd9697c142b3aa544ee243a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554683"
---
# <a name="get-request-and-response-schemas"></a>获取请求和响应架构


下面是 Get 请求架构和相应的响应架构定义和各自的示例。

## <a name="the-get-request-schema"></a>Get 请求架构


Get 请求和响应用于查询打印机的一个或多个其当前值。

在此示例中，有三个查询。 第一个查询是指向特定的双向通信架构值和第二个定义的子树的双向通信架构属性。 第三个是故意的错误： 没有任何&lt;Foo&gt;双向通信架构中的属性。 (下一节中对此请求的响应是[获取响应架构](#get-response-schema)。)

```xml
<bidi:Get xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.Configuration.DuplexUnit:Installed'/>
  <Query schema='\Printer.Configuration.HardDisk'/>
  <Query schema='\Printer.Foo'/>
</bidi:Get>
```

Get 请求架构中的正式定义

```xml
<?xml version='1.0'?>
<schema targetNamespace="http://schemas.microsoft.com/windows/2005/03/printing/bidi"
  xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='http://www.w3.org/2001/XMLSchema'>
  <element name='Get'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Query'>
          <complexType>
            <attribute name='schema' type='bidi:PARTIAL_SCHEMA_STRING' use='required'/>
            <anyAttribute namespace='##other' processContents='skip'/>
          </complexType>
        </element>
      </sequence>
      <anyAttribute namespace='##other' processContents='skip'/>
    </complexType>
  </element>
  <simpleType name='PARTIAL_SCHEMA_STRING'>
    <restriction base='string'>
      <pattern value='\(\w+(\.\w+)*(\:\w+)?)?'/>
    </restriction>
  </simpleType>
</schema>
```

## <a name="the-get-response-schema"></a>获取响应架构


此示例是对上面的 Get 请求的响应。 对于查询该成功，结果是值的特定架构。 第三个查询失败，因此结果是一个错误代码。 请注意第二个查询请求具有子级的属性，因为响应提供的名称和值的所有子级。

```xml
<bidi:Get xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.Configuration.DuplexUnit:Installed'/>
    <Schema name='\Printer.Configuration.DuplexUnit:Installed'>
      <BIDI_BOOL>true</BIDI_BOOL>
    </Schema>
  </Query>
  <Query schema='\Printer.HardDisk'>
    <Schema name='\Printer.HardDisk:Installed'>
      <BIDI_BOOL>true</BIDI_BOOL>
    </Schema>
    <Schema name='\Printer.HardDisk:Capacity'>
      <BIDI_INT>20971520</BIDI_INT>
    </Schema>
    <Schema name='\Printer.HardDisk:FreeSpace'>
      <BIDI_INT>10460419</BIDI_INT>
    </Schema>
  </Query>
  <Query schema='\Printer.Foo'>
    <Error>ERROR_BIDI_SCHEMA_NOT_SUPPORTED</Error>
  </Query>
</bidi:Get>
```

获取响应架构中的正式定义

```xml
<?xml version='1.0'?>
<schema targetNamespace="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='http://www.w3.org/2001/XMLSchema'>
  <element name='Get'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Query'>
          <complexType>
            <choice>
              <sequence maxOccurs='unbounded'>
                <element name='Schema'>
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
                    <attribute name='name' type='bidi:SCHEMA_STRING' use='required'/>
                  </complexType>
                </element>
              </sequence>
              <element name='Error' type='integer'/>
            </choice>
            <attribute name='schema' type='bidi:PARTIAL_SCHEMA_STRING' use='required'/>
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
  <simpleType name='PARTIAL_SCHEMA_STRING'>
    <restriction base='string'>
      <pattern value='\(\w+(\.\w+)*(\:\w+)?)?'/>
    </restriction>
  </simpleType>
</schema>
```

## <a name="related-topics"></a>相关主题

[双向通信架构](bidirectional-communication-schema.md)  

[SendRecvXMLStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)  
