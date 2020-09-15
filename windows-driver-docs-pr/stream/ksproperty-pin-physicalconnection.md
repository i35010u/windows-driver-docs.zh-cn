---
title: KSPROPERTY \_ PIN \_ PHYSICALCONNECTION
description: 音频适配器驱动程序使用 KSPROPERTY \_ 引脚 \_ PHYSICALCONNECTION 属性来表示微型端口之间的物理连接。
ms.assetid: a679ce41-93d2-4b46-a26d-ce05408ec6aa
keywords:
- KSPROPERTY_PIN_PHYSICALCONNECTION 流媒体设备
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
ms.openlocfilehash: 2fd873f52d0e354f2643e5d115b20afb27fcecf5
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104416"
---
# <a name="ksproperty_pin_physicalconnection"></a>KSPROPERTY \_ PIN \_ PHYSICALCONNECTION


音频适配器驱动程序使用 KSPROPERTY \_ 引脚 \_ PHYSICALCONNECTION 属性来表示微型端口之间的物理连接。

## <span id="ddk_ksproperty_pin_physicalconnection_ks"></span><span id="DDK_KSPROPERTY_PIN_PHYSICALCONNECTION_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

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
<th>获取</th>
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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kspin_physicalconnection" data-raw-source="[&lt;strong&gt;KSPIN_PHYSICALCONNECTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_physicalconnection)"><strong>KSPIN_PHYSICALCONNECTION</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

使用 KSP pin 指定此属性 \_ ，其中成员指定相关的 PIN 工厂。

KSPROPERTY \_ PIN \_ PHYSICALCONNECTION 返回 [**KSPIN \_ PHYSICALCONNECTION**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_physicalconnection)类型的结构，指定连接的 **PinId** 和连接的筛选器的符号链接名称。

类驱动程序不处理此属性;stream 微型驱动程序必须自行提供处理。

音频适配器驱动程序将连接注册到 [**PcRegisterPhysicalConnection**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)。

随后，SysAudio 系统驱动程序 (*sysaudio.sys*) 查询此属性并相应地生成图形。 SysAudio 使用此属性来确定哪些 wave 筛选器 pin 连接到哪些拓扑筛选器 pin。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSPIN \_ PHYSICALCONNECTION**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_physicalconnection)

[**PcRegisterPhysicalConnection**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)

