---
title: 自动检测 PPD 的双工单元
description: 自动检测 PPD 的双工单元
keywords:
- 自动检测双工单元 WDK 打印机自动配置
- PPD 文件 WDK 自动配置，自动检测双工单元
- 内置自动配置支持 WDK 打印机，自动检测双工单元
- 检测双工单元
- 双工单元 WDK 打印机自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e920f3472629b27fe72c6f2f2308d669b3ed15b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797857"
---
# <a name="autodetect-the-duplex-unit-for-ppd"></a>自动检测 PPD 的双工单元


以下两个示例显示了双工单元功能之间的一种可能的映射，如 PPD 文件中所述，以及它在 GDL 文件中的对应项。 此第一个示例摘自 PPD 文件。

```PPD
*OpenUI *DuplexUnit: Boolean
*DefaultDuplexUnit: True
*DuplexUnit True/Installed: ""
*DuplexUnit False/Not Installed: ""
*?DuplexUnit: "
  save
    currentpagedevice /Duplex known
    {(True)}{(False)}ifelse = flush
  restore
"
*End
*CloseUI: *DuplexUnit
```

下一个示例摘自 GDL 文件，并显示与上一示例中的双工单元功能对应的 DuplexUnit 功能定义。

```GDL
*Feature: DuplexUnit
{
  *FeatureType: PRINTER_PROPERTY

  *% *BidiQuery and *BidiResponse constructs must have the same names
  *BidiQuery: DuplexUnit
  {
    *QueryString: "\Printer.Configuration.DuplexUnit:Installed"
  }
  *BidiResponse: DuplexUnit
  {
    *ResponseType: BIDI_BOOL
    *ResponseData: ENUM_OPTION (DuplexUnit)
  }

  *Option: False
  {
    *BidiValue: BOOL(FALSE)
  }
  *Option: True
  {
    *BidiValue: BOOL(TRUE)
  }
}
```

 

 




