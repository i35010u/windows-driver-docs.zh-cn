---
title: 自动检测 GPD 的双工单元
description: 自动检测 GPD 的双工单元
keywords:
- 自动检测双工单元 WDK 打印机自动配置
- GPD 文件 WDK GDL 扩展，自动检测双工单元
- 内置自动配置支持 WDK 打印机，自动检测双工单元
- 检测双工单元
- 双工单元 WDK 打印机自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1329f5db7d0d685a28d48f3cb2e300463bb70da5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797853"
---
# <a name="autodetecting-the-duplex-unit-for-gpd"></a>自动检测 GPD 的双工单元


假设你的 GPD 文件有一个双工功能，该功能按如下示例所示进行定义，以便可以安装双工单元：

```GPD
*Feature: Duplex
{
   *rcNameID: =TWO_SIDED_PRINTING_DISPLAY
  *DefaultOption: NONE
  *Option: NONE
  {
    *rcNameID: =NONE_DISPLAY
    *Command: CmdSelect
    {
      *Order: DOC_SETUP.9
      *Cmd: "<1B>&l0S"
    }
  }
  *Option: VERTICAL
  {
    *rcNameID: =FLIP_ON_LONG_EDGE_DISPLAY
    *Command: CmdSelect
    {
      *Order: DOC_SETUP.10
      *Cmd: "<1B>&l1S"
    }
  }
  *Option: HORIZONTAL
  {
    *rcNameID: =FLIP_ON_SHORT_EDGE_DISPLAY
    *Command: CmdSelect
    {
      *Order: DOC_SETUP.10
      *Cmd: "<1B>&l2S"
    }
  }
}

*%
*% Installable Option
*%
*Feature: DuplexUnit
{
  *rcNameID: 429 *% Duplex Unit
  *HelpIndex: 12004
  *FeatureType: PRINTER_PROPERTY
  *DefaultOption: FALSE
  *Option: NotInstalled
  {
    *rcNameID: 444
    *DisabledFeatures: LIST(Duplex.VERTICAL, Duplex.HORIZONTAL)
  }
  *Option: Installed
  {
    *rcNameID: 443
  }
}
```

下面的 GDL 代码示例提供了自动检测双工单元 (的功能，这在前面的 GPD 代码示例) 中介绍，并设置相应的选项。 在此示例中，后台处理程序发送在 BidiQuery 构造中显示的查询 \* **BidiQuery** 。 当打印机收到查询时，它将以两个可能的 \* *_选项_* 构造值之一来响应。

```GDL
*Feature: DuplexUnit
{
  *% Note that the *BidiQuery and *BidiResponse constructs must have the same names
  *BidiQuery: DuplexUnit
  {
    *QueryString: "\Printer.Configuration.DuplexUnit:Installed"
  }

  *BidiResponse: DuplexUnit
  {
    *ResponseType: BIDI_BOOL
    *ResponseData: ENUM_OPTION(DuplexUnit)
  }

  *Option: NotInstalled
  {
    *BidiValue: BOOL(FALSE)
  }

  *Option: Installed
  {
    *BidiValue: BOOL(TRUE)
  }
}
```








