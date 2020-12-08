---
title: 自动检测 PPD 的打印机硬盘驱动器
description: 自动检测 PPD 的打印机硬盘驱动器
keywords:
- 自动检测打印机硬盘驱动器 WDK 打印机自动配置
- PPD 文件 WDK 自动配置，自动检测硬盘驱动器
- 内置自动配置支持 WDK 打印机，自动检测硬盘驱动器
- 检测打印机硬盘驱动器
- 硬盘自动检测 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbd7ed4460e85389e0d1ea455b23754db2945765
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797851"
---
# <a name="autodetect-the-printers-hard-drive-for-ppd"></a>自动检测 PPD 的打印机硬盘驱动器


向 GDL 文件中添加用于 PPD 文件中任何硬盘相关功能的条目。 为此，可以使用上一示例中所示的相同技术，在 GDL 文件中创建相应的功能构造。 以下 GDL 构造自动检测是否安装了硬盘。

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

 

 




