---
title: pciir
description: Pciir 扩展显示硬件路由外围组件互连 (PCI) 设备，以中断控制器输入的内容。
ms.assetid: 83d1b716-adfe-4712-bdbb-25960c38fff0
keywords:
- PCI IRQ 路由表
- 外围组件互连 (PCI)
- pciir Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pciir
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3fc18822b946a2d64f755ab14888ecb35ccca71d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335805"
---
# <a name="pciir"></a>!pciir


**！ Pciir**扩展显示硬件路由外围组件互连 (PCI) 设备，以中断控制器输入的内容。

```dbgcmd
!pciir
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p>
<p><strong>Windows Server 2003</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Vista 及更高版本</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

此扩展命令仅用于不具有高级配置和电源接口 (ACPI) 启用的基于 x86 的目标计算机。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

任何已启用 ACPI 的计算机上的类似信息，请使用[ **！ acpiirqarb** ](-acpiirqarb.md)扩展。

有关 PCI 总线的信息，请参阅 Windows Driver Kit (WDK) 文档。

 

 





