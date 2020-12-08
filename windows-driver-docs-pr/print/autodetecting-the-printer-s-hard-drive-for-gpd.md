---
title: 自动检测 GPD 的打印机硬盘驱动器
description: 自动检测 GPD 的打印机硬盘驱动器
keywords:
- 自动检测打印机硬盘驱动器 WDK 打印机自动配置
- GPD 文件 WDK GDL 扩展，自动检测硬盘驱动器
- 内置自动配置支持 WDK 打印机，自动检测硬盘驱动器
- 检测打印机硬盘驱动器
- 硬盘自动检测 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3383a7c8a1e5a00a99c21f42bbc3a225d9652f2b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797841"
---
# <a name="autodetecting-the-printers-hard-drive-for-gpd"></a>自动检测 GPD 的打印机硬盘驱动器


将条目添加到 GDL 文件，以获取 GPD 文件中任何与硬盘相关的功能。 例如，如果您的逐份打印功能取决于是否安装了硬盘驱动器，则可以使用自动配置功能自动确定打印机是否能够进行分页。 请考虑 GPD 文件中的以下代码示例。

```GPD
*% Printer supports collation only if PrinterHardDisk is installed
*Feature: Collate
{
  *rcNameID: 392 

  *DefaultOption: OFF
  *Option: ON
  {
    *rcNameID: =ON_DISPLAY
    *switch: PrinterHardDisk
    {
      *case: FALSE
      {
        *Command: CmdSelect
        {
           *Order: JOB_SETUP.5
           *% Collate requested but no disk =>
           *%   printer collate disabled
           *% Print Processor will take care
           *%   of collated copies

           *Cmd: ""
         }
      }
      *case: TRUE
      {
        *Command: CmdSelect
        {
           *Order: JOB_SETUP.5
           *% Collate requested with disk => 
            *%   printer collate enabled
           *% Printer will take care of collated copies

           *Cmd: "@PJL SET QTY=" %d{NumOfCopies}"<0A>"
        }
      }
    }
  }
  *Option: OFF
  {
    *rcNameID: =OFF_DISPLAY
    *Command: CmdSelect
    {
      *Order: JOB_SETUP.5
      *Cmd: ""
    }
  }
}

*% Feature to explicitly constrain the Collate feature
*Feature: PrinterHardDisk
{
  *rcNameID: 430 *% Printer Hard Disk
  *HelpIndex: 12002
  *FeatureType: PRINTER_PROPERTY
  *DefaultOption: FALSE
  *Option: FALSE
  {
    *rcNameID: 444
    *DisabledFeatures: Collate.ON
  }
  *Option: TRUE
  {
    *rcNameID: 443
  }
}
```

若要自动检测是否已安装硬盘，并相应地启用或禁用排序，只需将下面的代码示例添加到 GDL 文件。

```GDL
*%The GDL parser merges this code with the corresponding feature construct in the GPD file
*Feature: PrinterHardDisk
{
  *% *BidiQuery and *BidiResponse constructs must have the same names
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








