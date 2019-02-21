---
title: 自动检测 PPD 双面打印单元
description: 自动检测 PPD 双面打印单元
ms.assetid: bbecceb1-ba1d-4d2d-9a7b-e43f49345ca2
keywords:
- 自动检测双面打印单元 WDK 打印机自动配置
- PPD 文件 WDK 自动配置，正在自动检测双面打印单元
- 框中自动配置支持 WDK 打印机，自动检测双面打印单元
- 检测双面打印单元
- 双面打印单元 WDK 打印机自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d808c550e226e0fc0eeb236aca9d0df79867936e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521387"
---
# <a name="autodetect-the-duplex-unit-for-ppd"></a>自动检测 PPD 双面打印单元


以下两个示例显示一个可能的双面打印单元功能之间的映射中 PPD 文件和对应的 GDL 文件中所述。 此第一个示例是 PPD 文件的摘录。

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

下一个示例是一段摘录 GDL 文件，并显示对应于前面的示例中的双面打印单元功能 DuplexUnit 功能定义。

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

 

 




