---
title: 自动检测 PPD 的打印机硬盘驱动器
description: 自动检测 PPD 的打印机硬盘驱动器
ms.assetid: 0f2eba5c-1a05-4aaf-8780-266d2339570e
keywords:
- 自动检测打印机硬盘驱动器 WDK 打印机自动配置
- PPD 文件 WDK 自动配置，正在自动检测硬盘驱动器
- 框中自动配置支持 WDK 打印机，自动检测硬盘驱动器
- 检测打印机硬盘驱动器
- 硬盘驱动器自动检测 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50ddc8db58ea8a5db956970fe4435b8ce4a078c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349259"
---
# <a name="autodetect-the-printers-hard-drive-for-ppd"></a>自动检测 PPD 的打印机硬盘驱动器


将条目添加到 PPD 文件中任何硬与驱动器有关功能的 GDL 文件。 可以通过使用在前面的示例所示的相同技术 GDL 文件中创建相应的功能构造来执行此操作。 以下 GDL 构造会自动检测是否已安装硬盘。

```GDL
*% The GDL parser merges this feature definition with the 
*% corresponding feature construct in the GPD file
*Feature: PrinterHardDisk
{
  *FeatureType: PRINTER_PROPERTY

  *BidiQuery: PrinterHardDisk
  {
     *QueryString: "\Printer.Configuration.HardDisk:Installed"
  }
  *BidiResponse: PrinterHardDisk
  {
     *ResponseType: BIDI_BOOL
     *ResponseData: ENUM_OPTION (PrinterHardDisk)
  }
  *Option: FALSE
  {
     *BidiValue: BOOL(FALSE)
  }
  *Option: TRUE
  {
     *BidiValue: BOOL(TRUE)
  }
}
```

 

 




