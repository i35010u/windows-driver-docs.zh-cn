---
title: PIN 打印的示例 PrintCapabilities 文件
description: 下面是示例 PrintCapabilities 文件以演示如何指定个人标识号 (PIN) 受保护的打印。
ms.assetid: 4C3BBEF1-C0DB-48F7-B4EC-BBB5D3699692
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1c674cdd09328183a57ede8759c07e46ea6f622
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354940"
---
# <a name="sample-printcapabilities-file-for-pin-printing"></a>PIN 打印的示例 PrintCapabilities 文件


下面是示例 PrintCapabilities 文件以演示如何指定个人标识号 (PIN) 受保护的打印。

```xml
<?xml version="1.0"?>
<psf:PrintCapabilities
   xmlns:psf="http://schemas.microsoft.com/windows/2003/08/printing/printschemaframework" 
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
   xmlns:xsd="http://www.w3.org/2001/XMLSchema" version="1"
   xmlns:psk="http://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
   xmlns:pskv11=" http://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11">
   <psf:ParameterDef name="pskv11:JobPasscodeString">
      <psf:Property name="psf:DataType">
           <psf:Value xsi:type="xsd:QName">xsd:string</psf:Value>
      </psf:Property>
      <psf:Property name="psf:DefaultValue">
           <psf:Value xsi:type="xsd:string"/>
      </psf:Property>
      <psf:Property name="psf:MaxLength">
           <psf:Value xsi:type="xsd:integer">9</psf:Value>
      </psf:Property>
      <psf:Property name="psf:MinLength">
           <psf:Value xsi:type="xsd:integer">4</psf:Value>
      </psf:Property>
      <psf:Property name="psf:Mandatory">
              <psf:Value xsi:type="xsd:QName">psk:Optional</psf:Value>
      </psf:Property>
      <psf:Property name="psf:UnitType">
              <psf:Value xsi:type="xsd:string">numeric</psf:Value>
      </psf:Property>
      <psf:Property name="psk:DisplayName">
           <psf:Value xsi:type="xsd:string">Job PassCode</psf:Value>
      </psf:Property>
   </psf:ParameterDef>
   <psf:Feature name="pskv11:JobPasscode">
      <psf:Property name="psf:SelectionType">
           <psf:Value xsi:type="xsd:string">psk:PickOne</psf:Value>
      </psf:Property>
      <psf:Property name="psk:DisplayName">
           <psf:Value xsi:type="xsd:string">Enable Job PassCode</psf:Value>
      </psf:Property>
      <psf:Option name="psk:On" />
      <psf:Option name="psk:Off" />
   </psf:Feature>
</psf:PrintCapabilities>
```

有关受保护的打印的详细信息，请参阅[驱动程序支持的受保护的打印](driver-support-for-protected-printing.md)。

 

 




