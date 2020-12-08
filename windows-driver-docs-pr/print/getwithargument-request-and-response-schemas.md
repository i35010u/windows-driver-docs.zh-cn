---
title: GetWithArgument 请求和响应架构
description: 下面是 GetWithArgument 请求架构和相应的响应架构定义以及每个定义的示例。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ea175b421352a55bde6e56bb7a7d6151fd1bac9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796893"
---
# <a name="getwithargument-request-and-response-schemas"></a>GetWithArgument 请求和响应架构


下面是 GetWithArgument 请求架构和相应的响应架构定义以及每个定义的示例。

## <a name="getwithargument-request-schema"></a>GetWithArgument 请求架构


GetWithArgument 请求用于查询打印机的一个或多个当前值。

对此请求的响应位于以下 [GetWithArgument 响应架构](#getwithargument-response-schema)部分。

```xml
<bidi:GetWithArgument xmlns:bidi='https://schemas.microsoft.com/windows/2005/03/printing/bidi'>
  <Query schema='\Printer.Resources:Data'>
    <BIDI_STRING>en-us</BIDI_STRING>
  </Query>
</bidi:GetWithArgument>
```

GetWithArgument 请求架构的正式定义

```xml
<?xml version='1.0'?>  
<schema targetNamespace='https://schemas.microsoft.com/windows/2005/03/printing/bidi'  
    xmlns:bidi='https://schemas.microsoft.com/windows/2005/03/printing/bidi'   
    xmlns ='https://www.w3.org/2001/XMLSchema'>  
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
<bidi:GetWithArgumentResponse xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
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
<schema targetNamespace='https://schemas.microsoft.com/windows/2005/03/printing/bidi'  
    xmlns:bidi='https://schemas.microsoft.com/windows/2005/03/printing/bidi'   
    xmlns ='https://www.w3.org/2001/XMLSchema'>  
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

[SendRecvXMLStream](/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)
