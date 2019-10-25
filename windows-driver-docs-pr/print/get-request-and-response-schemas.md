---
title: 获取请求和响应架构
description: 下面是 Get 请求架构和相应的响应架构定义以及每个定义的示例。
ms.assetid: 48980220-4DD6-4785-AAC1-850F8FBE49EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93965c0096d702bbfb6fefe53034265420db9453
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844513"
---
# <a name="get-request-and-response-schemas"></a>获取请求和响应架构

下面是 Get 请求架构和相应的响应架构定义以及每个定义的示例。

## <a name="the-get-request-schema"></a>Get 请求架构

Get 请求和响应用于查询打印机的一个或多个当前值。

在此示例中，有三个查询。 第一个查询指向特定的双向通信架构值，第二个查询用于定义子树的双向通信架构属性。 第三个错误是：双向通信架构中没有 &lt;Foo&gt; 属性。 （对此请求的响应位于[获取响应架构](#the-get-response-schema)的下一节中。）

```xml
<bidi:Get xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema='\Printer.Configuration.DuplexUnit:Installed'/>
  <Query schema='\Printer.Configuration.HardDisk'/>
  <Query schema='\Printer.Foo'/>
</bidi:Get>
```

Get 请求架构的正式定义

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

此示例是对上述 Get 请求的响应。 对于成功的查询，结果为特定架构的值。 第三个查询失败，因此结果为错误代码。 请注意，由于第二个查询请求了具有子级的属性，因此响应提供所有子级的名称和值。

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

获取响应架构的正式定义

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

[SendRecvXMLStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)  
