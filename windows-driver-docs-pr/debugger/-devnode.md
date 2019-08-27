---
title: devnode
description: Devnode 扩展显示有关设备树中的节点的信息。
ms.assetid: 0c8cb743-f756-461e-b92b-352b550706c1
keywords:
- 设备节点
- 设备树
- devnode Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- devnode
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f912b91657f078310d6635196fb0685b7fd5d2c4
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025271"
---
# <a name="devnode"></a>!devnode


**! Devnode** extension 显示设备树中节点的相关信息。

```dbgcmd
!devnode Address [Flags] [Service]  
!devnode 1 
!devnode 2
```

## <a name="span-idddk__devnode_dbgspanspan-idddk__devnode_dbgspanparameters"></a><span id="ddk__devnode_dbg"></span><span id="DDK__DEVNODE_DBG"></span>Parameters


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要显示其节点的设备扩展的十六进制地址。 如果此值为零, 则显示主设备树的根。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定要显示的输出级别。 这可以是以下位的任意组合:

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
使显示包含设备节点的所有子级。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
使显示包含已使用的资源 (CM\_资源\_列表)。 \_其中包括 irp MN\_查询\_资源报告的启动配置, 以及 irp\_MN\_的*AllocatedResources*参数中分配给该设备的资源。启动\_设备。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
\_使显示包含 IRP\_\_MN\_筛选器资源\_需求报告的所需资源 (IO 资源需求列表)。\_\_

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
导致显示在 IRP\_MN\_启动\_设备的*AllocatedResourcesTranslated*参数中包括已分配给设备的已转换资源列表。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>位 4 (0x10)  
指定仅显示未启动的设备节点。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>位 5 (0x20)  
指定只显示有问题的设备节点。 (这些节点包含标志位 DNF\_有\_问题或 DNF\_有\_私有\_问题。)

<span id="_______Service______"></span><span id="_______service______"></span><span id="_______SERVICE______"></span>*服务*   
指定服务的名称。 如果包括此服务, 则只会显示此服务驱动的设备节点。 (如果*标志*包含位 0x1, 则会显示此服务所驱动的设备节点及其所有子节点。)

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Kdexts</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

请参阅[即插即用调试](plug-and-play-debugging.md)此扩展命令的应用程序。 有关设备树的详细信息, 请参阅 Windows 驱动程序工具包 (WDK) 文档和*Microsoft Windows 内部*Russinovich, 并将其标记为 "" 和 "David"。

<a name="remarks"></a>备注
-------

**! Devnode 1**命令列出设备对象的所有挂起的删除。

**! Devnode 2**命令列出了设备对象的所有挂起的弹出。

可以使用 **! devnode 0 1**查看整个设备树。

 

 





