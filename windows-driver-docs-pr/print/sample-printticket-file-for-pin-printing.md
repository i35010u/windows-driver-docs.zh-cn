---
title: PIN 打印的示例 PrintTicket 文件
description: 下面是一个示例 PrintTicket 文件，用于说明如何指定 PIN 打印。
ms.assetid: FC1BE797-7097-4BEF-A530-3846CED3E400
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27fcf3eaad6fc7935a952a7994972c7c50f0b50e
ms.sourcegitcommit: ab64169b631da4db3f0b895600f1c38a22cb7e2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/03/2020
ms.locfileid: "75652963"
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

有关受保护打印的详细信息，请参阅[受保护打印的驱动程序支持](driver-support-for-protected-printing.md)。

 

 




