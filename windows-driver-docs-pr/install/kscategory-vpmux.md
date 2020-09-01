---
title: KSCATEGORY_VPMUX
description: KSCATEGORY_VPMUX
ms.assetid: d63ecb2b-f1f7-4f02-a82e-4ed17d1f83d9
keywords:
- KSCATEGORY_VPMUX 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_VPMUX
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e47416e8a77a9b4c19b07b9f6a73cb0f0afb1a6b
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097341"
---
# <a name="kscategory_vpmux"></a>KSCATEGORY_VPMUX


为支持视频多路复用的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_VPMUX[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_VPMUX</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{A799A803-A46D-11D0-A18C-00A02401DCD4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_VPMUX 的实例，以向操作系统指示设备支持 KSCATEGORY_VPMUX 功能类别。

有关视频设备的常规信息，请参阅 [视频捕获设备](../stream/video-capture-devices.md)。

有关视频设备的设备接口类的信息，请参阅 [**KSCATEGORY_VIDEO**](kscategory-video.md)。

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


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

