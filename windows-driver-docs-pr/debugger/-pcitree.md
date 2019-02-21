---
title: pcitree
description: Pcitree 扩展显示有关 PCI 设备对象，包括子 PCI 总线和 CardBus 总线，以及连接到它们的设备的信息。
ms.assetid: cd1b2f85-b8de-4396-8b37-79bb3d62092c
keywords:
- PCI 总线
- PCI 设备
- pcitree Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- pcitree
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ec6a45831e8f04d9b6cf7b6ba66fb57622e5fb7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526469"
---
# <a name="pcitree"></a>！ pcitree


**！ Pcitree**扩展显示有关 PCI 设备对象，包括子 PCI 总线和 CardBus 总线的信息和设备连接到它们。

```dbgcmd
!pcitree
```

## <span id="ddk__pcitree_dbg"></span><span id="DDK__PCITREE_DBG"></span>


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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 有关 PCI 总线和 PCI 设备对象的信息，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

下面是一个示例：

```dbgcmd
kd> !pcitree

Bus 0x0 (FDO Ext fe517338)
  0600 12378086 (d=0,  f=0) devext fe4f4ee8 Bridge/HOST to PCI
  0601 70008086 (d=d,  f=0) devext fe4f4ce8 Bridge/PCI to ISA
  0101 70108086 (d=d,  f=1) devext fe4f4ae8 Mass Storage Controller/IDE
  0604 00211011 (d=e,  f=0) devext fe4f4788 Bridge/PCI to PCI

Bus 0x1 (FDO Ext fe516998)
  0200 905010b7 (d=8,  f=0) devext fe515ee8 Network Controller/Ethernet
  0100 81789004 (d=9,  f=0) devext fe515ce8 Mass Storage Controller/SCSI
  0300 0519102b (d=10, f=0) devext fe4f4428 Display Controller/VGA

Total PCI Root busses processed = 1
```

若要了解此显示，请考虑最终的设备所示。 其基本类为 03、 其子类为 00、 设备 ID 是 0x0519，和其供应商 ID 是 0x102B。 这些值是所有设备本身内部函数。

之后的数字"d ="是设备号;之后的数字"f ="是函数数。 后"devext"是设备扩展 address，0xFE4F4428。 最后，基类名称和子类名称将出现。

若要获取有关设备的详细信息，请使用[ **！ devext** ](-devext.md)设备扩展地址作为自变量的扩展命令。 此特定设备，将为要使用的命令：

```dbgcmd
kd> !devext fe4f4428 pci 
```

如果 **！ pcitree**扩展插件将生成的错误，这通常意味着 PCI 符号未正确加载。 使用[ **.reload pci.sys** ](-reload--reload-module-.md)若要解决此问题。

 

 





