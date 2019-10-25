---
title: GetWithArgument 请求和响应架构
description: 下面是 GetWithArgument 请求架构和相应的响应架构定义以及每个定义的示例。
ms.assetid: F68731BC-2907-4FA2-B5A4-0FAC0A9F663A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d197342049aa9e50188e06736f033c8a12d671e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844584"
---
# <a name="getwithargument-request-and-response-schemas"></a>GetWithArgument 请求和响应架构


下面是 GetWithArgument 请求架构和相应的响应架构定义以及每个定义的示例。

## <a name="getwithargument-request-schema"></a>GetWithArgument 请求架构


GetWithArgument 请求用于查询打印机的一个或多个当前值。

对此请求的响应位于以下[GetWithArgument 响应架构](#getwithargument-response-schema)部分。

```xml
<bidi:GetWithArgument xmlns:bidi='http://schemas.microsoft.com/windows/2005/03/printing/bidi'>
  <Query schema='\Printer.Resources:Data'>
    <BIDI_STRING>en-us</BIDI_STRING>
  </Query>
</bidi:GetWithArgument>
```

GetWithArgument 请求架构的正式定义

```xml
<?xml version='1.0'?>  
<schema targetNamespace='http://schemas.microsoft.com/windows/2005/03/printing/bidi'  
    xmlns:bidi='http://schemas.microsoft.com/windows/2005/03/printing/bidi'   
    xmlns ='http://www.w3.org/2001/XMLSchema'>  
    <element name='GetWithArgument'>  
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
                        <attribute name='schema' type='bidi:PARTIAL_SCHEMA_STRING' use='required'/>  
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
    <simpleType name='PARTIAL_SCHEMA_STRING'>  
        <restriction base='string'>  
            <pattern value='\(\w+(\.\w+)*(\:\w+)?)?'/>  
        </restriction>  
    </simpleType>   
</schema>
```

## <a name="getwithargument-response-schema"></a>GetWithArgument 响应架构

此示例是对上述 GetWithArgument 请求的响应。 对于成功的查询，结果为特定架构的值。 如果查询失败，则结果为错误代码。

```xml
<bidi:GetWithArgumentResponse xmlns:bidi="http://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Query schema="\Printer.Data:GetWithArgument">
    <Schema name="\Printer.Data:GetWithArgument">
      <BIDI_BLOB>Base64 Encoded XML resource file data to be used by Print Config<BIDI_BLOB>
    </Schema>
  </Query>
</bidi:GetWithArgumentResponse>
```

GetWithArgument 响应架构的正式定义

```xml
<?xml version='1.0'?>  
<schema targetNamespace='http://schemas.microsoft.com/windows/2005/03/printing/bidi'  
    xmlns:bidi='http://schemas.microsoft.com/windows/2005/03/printing/bidi'   
    xmlns ='http://www.w3.org/2001/XMLSchema'>  
    <element name='GetWithArgumentResponse'>  
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
                                            <element name='Error'       type='integer'/>  
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
