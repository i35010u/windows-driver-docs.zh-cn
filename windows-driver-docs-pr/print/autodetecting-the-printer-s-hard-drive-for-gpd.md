---
title: 自动检测 GPD 的打印机硬盘驱动器
description: 自动检测 GPD 的打印机硬盘驱动器
ms.assetid: c3bc415e-fa4d-42d0-9686-3105a588a7ea
keywords:
- 自动检测打印机硬盘驱动器 WDK 打印机自动配置
- GPD 文件 WDK GDL 扩展，自动检测硬盘驱动器
- 框中自动配置支持 WDK 打印机，自动检测硬盘驱动器
- 检测打印机硬盘驱动器
- 硬盘驱动器自动检测 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54409b51cd6d1ea1a1aee0a8faf3db8e47d91587
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349254"
---
# <a name="autodetecting-the-printers-hard-drive-for-gpd"></a>自动检测 GPD 的打印机硬盘驱动器


将条目添加到 GPD 文件中任何硬与驱动器有关功能的 GDL 文件。 例如，如果您有取决于是否安装了硬盘驱动器的逐份打印功能，可以使用自动配置来自动确定打印机是否能够逐份打印。 请考虑下面的代码示例从 GPD 文件。

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

若要自动检测是否已安装硬盘，并启用或禁用排序规则相应地，只需将添加到 GDL 文件下面的代码示例。

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








