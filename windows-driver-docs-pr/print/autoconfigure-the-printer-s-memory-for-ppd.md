---
title: 自动配置 PPD 的打印机内存
description: 自动配置 PPD 的打印机内存
ms.assetid: 75df1026-896f-4840-a69d-975f813ca636
keywords:
- 内存 WDK 打印机自动配置
- PPD 文件 WDK 自动配置内存
- 框中自动配置支持 WDK 打印机，内存
- autoconfiguring 打印机内存 WDK
- 打印机内存配置 WDK 自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52037f4a9f90823f2d9130110a24ac7e584278a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350753"
---
# <a name="autoconfigure-the-printers-memory-for-ppd"></a>自动配置 PPD 的打印机内存


将条目添加到 PPD.中指定的内存选项 GDL 第一个示例是与可安装的内存选项 PPD 文件的示例摘录：

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

若要为"InstalledMemory"PPD 启用自动配置功能，请添加以下代码示例 GDL 文件。

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

 

 




