---
title: KSPROPERTY\_PIN\_PHYSICALCONNECTION
description: 音频适配器驱动程序使用 KSPROPERTY\_PIN\_PHYSICALCONNECTION 属性来表示微型端口之间的物理连接。
ms.assetid: a679ce41-93d2-4b46-a26d-ce05408ec6aa
keywords:
- KSPROPERTY_PIN_PHYSICALCONNECTION 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_PHYSICALCONNECTION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 703931775a142b58171de66a402dd6680243395c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380809"
---
# <a name="kspropertypinphysicalconnection"></a>KSPROPERTY\_PIN\_PHYSICALCONNECTION


音频适配器驱动程序使用 KSPROPERTY\_PIN\_PHYSICALCONNECTION 属性来表示微型端口之间的物理连接。

## <span id="ddk_ksproperty_pin_physicalconnection_ks"></span><span id="DDK_KSPROPERTY_PIN_PHYSICALCONNECTION_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563539" data-raw-source="[&lt;strong&gt;KSPIN_PHYSICALCONNECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563539)"><strong>KSPIN_PHYSICALCONNECTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

指定此属性使用 KSP\_PIN，其中该成员指定相关 pin 工厂。

KSPROPERTY\_PIN\_PHYSICALCONNECTION 返回类型的结构[ **KSPIN\_PHYSICALCONNECTION**](https://msdn.microsoft.com/library/windows/hardware/ff563539)，指定连接**PinId**和连接筛选器的符号链接名称。

在类驱动程序不处理此属性;流微型驱动程序必须提供自己的处理。

音频适配器驱动程序注册与的连接[ **PcRegisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537726)。

随后，SysAudio 系统驱动程序 (*sysaudio.sys*) 查询此属性，并相应地生成关系图。 SysAudio 使用此属性来确定哪个批筛选器插针连接到的拓扑的筛选器 pin。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSPIN\_PHYSICALCONNECTION**](https://msdn.microsoft.com/library/windows/hardware/ff563539)

[**PcRegisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537726)

 

 






