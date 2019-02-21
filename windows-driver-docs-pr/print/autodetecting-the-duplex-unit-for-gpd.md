---
title: 自动检测 GPD 双面打印单元
description: 自动检测 GPD 双面打印单元
ms.assetid: a5c91b00-ca7c-4c22-a16c-a976011d8b89
keywords:
- 自动检测双面打印单元 WDK 打印机自动配置
- GPD 文件 WDK GDL 扩展，自动检测双面打印单元
- 框中自动配置支持 WDK 打印机，自动检测双面打印单元
- 检测双面打印单元
- 双面打印单元 WDK 打印机自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13822ae9ded4430943a937ad182cfd383a3bb8e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524868"
---
# <a name="autodetecting-the-duplex-unit-for-gpd"></a>自动检测 GPD 双面打印单元


假设 GPD 文件具有一个双工功能，如以下示例定义，以便双面打印单元是可安装：

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

下面的 GDL 代码示例提供了自动检测存在双面打印单元 （这前面 GPD 代码示例中所述） 的功能，并设置相应的选项。 在此示例中，后台处理程序将发送的查询中所示\* **BidiQuery**构造。 当打印机收到查询时，响应其中一个的两个可能\***选项**构造的值。

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








