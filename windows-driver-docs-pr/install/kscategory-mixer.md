---
title: KSCATEGORY_MIXER
description: KSCATEGORY_MIXER
ms.assetid: b17696ed-d8d6-4d02-a23b-64ebc8505afd
keywords:
- KSCATEGORY_MIXER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_MIXER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7192207246a4a261fd2fdc1db63ad3ee9fc7b0ac
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095007"
---
# <a name="kscategory_mixer"></a>KSCATEGORY_MIXER


为混合数据流 (KS) 功能类别定义的[内核流式处理](../stream/streaming-minidrivers2.md)KSCATEGORY_MIXER[设备接口类](./overview-of-device-interface-classes.md)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>KSCATEGORY_MIXER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{AD809C00-7B88-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_MIXER 的实例，以向操作系统指示设备支持 KSCATEGORY_MIXER 功能类别。

有关此功能类别和其他功能类别的详细信息，请参阅 [安装音频适配器的设备接口](../audio/installing-device-interfaces-for-an-audio-adapter.md) 和 [**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](../stream/ksproperty-topology-categories.md)

 

