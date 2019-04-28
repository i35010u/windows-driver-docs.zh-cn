---
title: acpicache
description: Acpicache 扩展显示所有缓存的 HAL 的高级配置和电源接口 (ACPI) 表。
ms.assetid: 488bbc40-0f67-4d13-8615-944ff8a6a177
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
ms.openlocfilehash: a5e2600a8a4d9b218e3c2153cf3d476c5861d46a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334826"
---
# <a name="acpicache"></a>!acpicache


**！ Acpicache**扩展将显示所有缓存的 HAL 的高级配置和电源接口 (ACPI) 表。

```dbgcmd
!acpicache [DisplayLevel]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______DisplayLevel______"></span><span id="_______displaylevel______"></span><span id="_______DISPLAYLEVEL______"></span> *DisplayLevel*   
指定显示的详细信息级别。 此值是缩写显示为 0 或 1 的更多详细显示。 默认值为 0。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

ACPI 有关的信息，请参阅 Microsoft Windows Driver Kit (WDK) 文档，Windows SDK 文档中，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些书籍和资源可能不可用在某些语言和国家/地区中。）另请参阅[ACPI 调试](acpi-debugging.md)ACPI 与相关联的其他扩展有关的信息。

 

 





