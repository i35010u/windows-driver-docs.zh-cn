---
title: KSCATEGORY_TVAUDIO
description: KSCATEGORY_TVAUDIO
ms.assetid: a3fac238-2712-4eef-b768-4bc2ac43ec4c
keywords:
- KSCATEGORY_TVAUDIO 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_TVAUDIO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3d397a694a6d34b0954d30508db07ba431d568db
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095804"
---
# <a name="kscategory_tvaudio"></a>KSCATEGORY_TVAUDIO


为 TV 音频设备的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_TVAUDIO[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_TVAUDIO</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{A799A802-A46D-11D0-A18C-00A02401DCD4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册此 KSCATEGORY_TVAUDIO 的实例，以向操作系统指示设备支持 KSCATEGORY_TVAUDIO 功能类别。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 WDK 的*src/swtuner/algtuner*目录中的软件调谐器示例附带的*Bdan* inf 文件。

有关视频设备的信息，请参阅 [视频捕获设备](../stream/video-capture-devices.md)、 [筛选器图示例](../stream/filter-graph-examples.md)和 [编码器设备](../stream/encoder-devices.md)。

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
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSCATEGORY_TVTUNER**](kscategory-tvtuner.md)

 

