---
title: EnumSchema 请求和响应架构
description: 下面是 EnumSchema 请求架构和相应的响应架构定义以及每个定义的示例。
ms.assetid: 031FA2EA-A33B-409C-82FD-B4FE9D0A2E93
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 798cc4d66e12e7627ca9747f55eb3c543b4e8075
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652799"
---
# <a name="enumschema-request-and-response-schemas"></a>EnumSchema 请求和响应架构


下面是 EnumSchema 请求架构和相应的响应架构定义以及每个定义的示例。

## <a name="the-enumschema-request-schema"></a>EnumSchema 请求架构


EnumSchema 请求用于获取打印机属性的列表。

所有 EnumSchema 请求都是完全相同的，只包含一个根元素。

```xml
<bidi:EnumSchema xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi"/>
```

EnumSchema 请求架构的正式定义

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='https://www.w3.org/2001/XMLSchema'>
  <element name='EnumSchema'>
    <complexType>
      <anyAttribute namespace='##other' processContents='skip'/>
    </complexType>
  </element>
</schema>
```

## <a name="the-enumschema-response-schema"></a>EnumSchema 响应架构


EnumSchema 响应具有每个属性的 &lt;架构&gt; 元素。

在此示例中，打印机只有几个可访问的属性。

```xml
<bidi:EnumSchema xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi">
  <Schema name='\Printer.Configuration.DuplexUnit:Installed' />
  <Schema name='\Printer.Configuration.HardDisk:Installed'/>
  <Schema name='\Printer.Configuration.HardDisk:Capacity'/>
  <Schema name='\Printer.Configuration.HardDisk:FreeSpace'/>
</bidi:EnumSchema>
```

EnumSchema 响应架构的正式定义

```xml
<?xml version='1.0'?>
<schema targetNamespace="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns:bidi="https://schemas.microsoft.com/windows/2005/03/printing/bidi" 
  xmlns ='https://www.w3.org/2001/XMLSchema'>
  <element name='EnumSchema'>
    <complexType>
      <sequence maxOccurs='unbounded'>
        <element name='Schema'>
          <complexType>
            <attribute name='name' type='bidi:SCHEMA_STRING' use='required'/>
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

[SendRecvXMLStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstream)  

[SendRecvXMLString](https://docs.microsoft.com/windows-hardware/drivers/ddi/bidispl/nf-bidispl-ibidispl2-sendrecvxmlstring)  



