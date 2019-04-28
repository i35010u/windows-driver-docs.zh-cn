---
title: devnode
description: Devnode 扩展显示设备树中节点的相关信息。
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
ms.openlocfilehash: 1d033ae27542c9a75445df6705f2a47fc99e06ce
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334587"
---
# <a name="devnode"></a>!devnode


**！ Devnode**扩展显示设备树中节点的相关信息。

```dbgcmd
!devnode Address [Flags] [Service]  
!devnode 1 
!devnode 2
```

## <a name="span-idddkdevnodedbgspanspan-idddkdevnodedbgspanparameters"></a><span id="ddk__devnode_dbg"></span><span id="DDK__DEVNODE_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定在其节点的显示设备扩展的十六进制地址。 如果这是零，将显示主要设备树的根。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
指定输出要显示的级别。 这可以是以下位的任意组合：

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>位 0 (0x1)  
将导致显示以包括设备节点的所有子级。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>位 1 (0x2)  
将导致显示以包括使用的资源 (CM\_资源\_列表)。 其中包括启动配置报告的 IRP\_MN\_查询\_资源，以及分配给该设备中的资源*AllocatedResources*参数 IRP\_MN\_启动\_设备。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>位 2 (0x4)  
将导致显示以包括所需的资源 (IO\_资源\_要求\_列表) 报告的 IRP\_MN\_筛选器\_资源\_要求。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>位 3 (0x8)  
显示要分配给该设备中包含翻译后的资源的列表将导致*AllocatedResourcesTranslated* IRP 参数\_MN\_启动\_设备。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>4 位 (0x10)  
指定应显示只有设备不会启动的节点。

<span id="Bit_5__0x20_"></span><span id="bit_5__0x20_"></span><span id="BIT_5__0X20_"></span>5 位 (0x20)  
指定应显示只有设备有问题的节点。 (这些是节点包含标志位 DNF\_HAS\_问题或 DNF\_HAS\_专用\_问题。)

<span id="_______Service______"></span><span id="_______service______"></span><span id="_______SERVICE______"></span> *服务*   
指定服务的名称。 如果包含，则将显示这些由此服务驱动的设备节点。 (如果*标志*包括位 0x1，通过此服务及其所有将显示其子级驱动的设备节点。)

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

请参阅[插调试](plug-and-play-debugging.md)对于此扩展命令的应用程序。 有关设备树的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

**！ Devnode 1**命令将列出所有挂起删除的设备对象。

**！ Devnode 2**所有挂起的设备对象的弹出的命令列表。

可以使用 **！ devnode 0 1**若要查看整个设备树。

 

 





