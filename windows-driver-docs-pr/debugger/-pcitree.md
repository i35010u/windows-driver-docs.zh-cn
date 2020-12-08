---
title: pcitree
description: Pcitree 扩展显示有关 PCI 设备对象的信息，包括子 PCI 总线和 CardBus 总线以及连接到它们的设备。
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
ms.openlocfilehash: 65fac3ae57db8526ecee0e634922622e84811852
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792021"
---
# <a name="pcitree"></a>!pcitree


**！ Pcitree** extension 显示有关 PCI 设备对象的信息，包括子 pci 总线和 CardBus 总线以及连接到它们的设备。

```dbgcmd
!pcitree
```

## <span id="ddk__pcitree_dbg"></span><span id="DDK__PCITREE_DBG"></span>


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
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅 [即插即用调试](plug-and-play-debugging.md) 此扩展命令的应用程序。 有关 PCI 总线和 PCI 设备对象的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档。

<a name="remarks"></a>备注
-------

以下是示例：

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

若要理解这种显示，请考虑最终显示的设备。 其基类为03，其子类为00，其设备 ID 为0x0519，其供应商 ID 为0x102B。 这些值全部都是设备本身内部的。

"D =" 后面的数字是设备号;"f =" 后面的数字是函数号。 在 "devext" 为设备扩展地址0xFE4F4428 之后。 最后，将显示基类名称和子类名称。

若要获取有关设备的详细信息，请使用带有设备扩展地址的 [**！ devext**](-devext.md) extension 命令作为参数。 对于此特定设备，要使用的命令为：

```dbgcmd
kd> !devext fe4f4428 pci 
```

如果 **！ pcitree** 扩展生成错误，这通常意味着 PCI 符号未正确加载。 使用 [**. 重载 pci.sys**](-reload--reload-module-.md) 以解决此问题。

 

 





