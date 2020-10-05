---
title: KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR
description: KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR
ms.assetid: 812a9ec8-3b9e-4cf8-bf69-3b849ff6402a
keywords:
- KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fe1b816300ecf822036195a5f98c80feaf737469
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733953"
---
# <a name="kscategory_microphone_array_processor"></a>KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR


KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR [设备接口类](./overview-of-device-interface-classes.md) 是为 [内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义的，该类别用于处理麦克风数组的输入。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{830A44F2-A32D-476B-BE97-42845673B35A}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR 的实例，以向操作系统指示设备支持 KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR 功能类别。

有关音频设备功能类别的详细信息，请参阅 [安装音频适配器的设备接口](../audio/installing-device-interfaces-for-an-audio-adapter.md) 和 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)。

有关如何在 Windows Vista 中处理麦克风阵列的详细信息，请参阅 Windows vista [中的麦克风阵列支持](/previous-versions/windows/hardware/design/dn613960(v=vs.85)) 和 [如何构建和使用适用于 Windows Vista 的麦克风阵列](/previous-versions/windows/hardware/design/dn613960(v=vs.85)) 白皮书。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows Vista、Windows Server 2003、Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)

