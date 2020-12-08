---
title: PIN 打印的示例 PrintTicket 文件
description: 下面是一个示例 PrintTicket 文件，用于说明如何指定 PIN 打印。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ddd6c44fe234a2a99a29e6b0ffb789aa5ccb22b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806947"
---
# <a name="sample-printticket-file-for-pin-printing"></a>PIN 打印的示例 PrintTicket 文件


下面是一个示例 PrintTicket 文件，用于说明如何指定 PIN 打印。

```xml
<?xml version="1.0"?>
   <psf:PrintTicket xmlns:psf="https://schemas.microsoft.com/windows/2003/08/printing/printschemaframework" 
      xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" 
      xmlns:xsd="https://www.w3.org/2001/XMLSchema" version="1" 
           xmlns:psk="https://schemas.microsoft.com/windows/2003/08/printing/printschemakeywords"
           xmlns:pskv11=" https://schemas.microsoft.com/windows/2013/05/printing/printschemakeywordsv11">
      <psf:ParameterInit name="pskv11:JobPasscodeString">
         <psf:Value xsi:type="xsd:string">123456</psf:Value>
      </psf:ParameterInit>
      <psf:Feature name="pskv11:JobPasscode">
         <psf:Option name="psk:On" />
      </psf:Feature>
   </psf:PrintTicket>
```

有关受保护打印的详细信息，请参阅 [受保护打印的驱动程序支持](driver-support-for-protected-printing.md)。

 

 




