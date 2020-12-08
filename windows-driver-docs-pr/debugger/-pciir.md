---
title: pciir
description: Pciir 扩展显示外围组件互连 (PCI) 设备到中断控制器输入的硬件路由的内容。
keywords:
- PCI IRQ 路由表
- " (PCI) 的外围组件互连"
- pciir Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pciir
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1114b111de87be526277e8dd533d2f0e66007c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792029"
---
# <a name="pciir"></a>!pciir


**！ Pciir** extension 显示外围组件互连 (PCI) 设备到中断控制器输入的硬件路由的内容。

```dbgcmd
!pciir
```

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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
<td align="left"><p><strong>Windows Vista 及更高版本</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
</tbody>
</table>

 

此扩展命令仅可用于没有启用了高级配置和电源接口 (ACPI) 的基于 x86 的目标计算机。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关任何启用了 ACPI 的计算机上的类似信息，请使用 [**！ acpiirqarb**](-acpiirqarb.md) 扩展。

有关 PCI 总线的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

 

 





