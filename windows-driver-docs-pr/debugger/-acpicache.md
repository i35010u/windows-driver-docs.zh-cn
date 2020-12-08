---
title: acpicache
description: Acpicache 扩展显示由 HAL 缓存 (ACPI) 表的所有高级配置和电源接口。
keywords:
- acpicache Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- acpicache
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c483aa5c62ab12ce4e11376837ebbad303b397bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800203"
---
# <a name="acpicache"></a>!acpicache


**！ Acpicache** extension 显示由 HAL 缓存 (ACPI) 表的所有高级配置和电源接口。

```dbgcmd
!acpicache [DisplayLevel]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span>*DisplayLevel*   
指定显示的详细信息级别。 对于简写显示，此值为 0; 对于更详细的显示，该值为1。 默认值为 0。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 ACPI 的信息，请参阅 Microsoft Windows 驱动程序工具包 (WDK) 文档、Windows SDK 文档和 *Microsoft Windows 内部* ，并将标记 Russinovich 和 David 所罗门群岛。  (在某些语言和国家/地区可能无法使用这些书籍和资源。 ) 还请参阅 [Acpi 调试](acpi-debugging.md) ，获取有关与 ACPI 关联的其他扩展的信息。

 

 





