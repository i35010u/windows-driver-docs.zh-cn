---
title: PIN 打印的示例 PrintCapabilities 文件
description: 下面是一个示例 PrintCapabilities 文件，用于说明如何指定 (PIN) 受保护打印的个人 ID 号。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36d8fcfb615580f07eac7ff4f652cb9be87057f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806965"
---
# <a name="sample-printcapabilities-file-for-pin-printing"></a>PIN 打印的示例 PrintCapabilities 文件


下面是一个示例 PrintCapabilities 文件，用于说明如何指定 (PIN) 受保护打印的个人 ID 号。

```xml
<?xml version="1.0"?>
<psf:PrintCapabilities
   xmlns:psf="https://schemas.microsoft.com/windows/2003/08/printing/printschemaframework" 
   xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" 
   xmlns:xsd="https://www.w3.org/2001/XMLSchema" version="1"
   xmlns:psk="https://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
   xmlns:pskv11=" https://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11">
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

有关受保护打印的详细信息，请参阅 [受保护打印的驱动程序支持](driver-support-for-protected-printing.md)。

 

 




