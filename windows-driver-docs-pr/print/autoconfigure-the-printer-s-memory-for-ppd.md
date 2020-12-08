---
title: 自动配置 PPD 的打印机内存
description: 自动配置 PPD 的打印机内存
keywords:
- 内存 WDK 打印机自动配置
- PPD 文件 WDK 自动配置，内存
- 内置自动配置支持 WDK 打印机，内存
- autoconfiguring 打印机内存 WDK
- 打印机内存配置 WDK 自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 644bd119942edc23eebdb46b1a29d7e48f6e5644
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797859"
---
# <a name="autoconfigure-the-printers-memory-for-ppd"></a>自动配置 PPD 的打印机内存


向 GDL 中为 PPD 指定的内存选项添加项。 第一个示例摘自 PPD 文件，该文件涉及可安装内存选项：

```PPD
*% === Installable Options ===========
*OpenGroup: InstallableOptions/Options Installed
 
*OpenUI *InstalledMemory/Memory Configuration: PickOne
*DefaultInstalledMemory: 24Meg
*InstalledMemory 24Meg/Standard 24 MB RAM: ""
*InstalledMemory 56Meg/56 MB Total RAM: ""
*InstalledMemory 72Meg/72 MB Total RAM: ""
*CloseUI: *InstalledMemory
 
*CloseGroup: InstallableOptions
```

若要启用 "InstalledMemory" PPD 功能的自动配置，请将下面的代码示例添加到 GDL 文件中。

```GDL
*% This feature definition merges with the definition in the PPD file
*% because both have the same name
*Feature: InstalledMemory
{
  *FeatureType: PRINTER_PROPERTY

  *% *BidiQuery and *BidiResponse constructs must have the same names
  *BidiQuery: InstalledMemory
  {
    *QueryString: "\Printer.Configuration.Memory:Size"
  }
  *BidiResponse: InstalledMemory
  {
    *ResponseType: BIDI_INT
    *ResponseData: ENUM_OPTION (InstalledMemory)
  }
 
  *Option: 24Meg
  { 
    *BidiValue: INT(24576)
  } 
  *Option: 56Meg
  {
    *BidiValue: INT(57344)
  }
  *Option: 72Meg
  {
    *BidiValue: INT(73728)
  }
}
```

 

 




