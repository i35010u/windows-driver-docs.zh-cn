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
ms.openlocfilehash: 9b98c362419475bc1f3b886e2da75f8bf88f0546
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387020"
---
# <a name="kscategorymicrophonearrayprocessor"></a>KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR


KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 功能类别，用于处理从麦克风阵列输入。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
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

KS 设备的驱动程序注册 KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR 向操作系统指示设备支持 KSCATEGORY_MICROPHONE_ARRAY_PROCESSOR 功能分类的实例。

有关音频设备的功能类别的详细信息，请参阅[音频适配器安装设备接口](https://docs.microsoft.com/windows-hardware/drivers/audio/installing-device-interfaces-for-an-audio-adapter)并[ **KSPROPERTY_TOPOLOGY_CATEGORIES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories).

有关如何处理 Windows Vista 上的麦克风阵列的详细信息，请参阅[Windows Vista 中的麦克风阵列支持](https://go.microsoft.com/fwlink/p/?linkid=120592)并[如何与生成和使用麦克风阵列适用于 Windows Vista 的](https://go.microsoft.com/fwlink/p/?linkid=120593)白皮书。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista、 Windows Server 2003、 Windows XP 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)

 

 






