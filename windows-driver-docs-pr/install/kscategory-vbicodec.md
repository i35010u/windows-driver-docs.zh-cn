---
title: KSCATEGORY_VBICODEC
description: KSCATEGORY_VBICODEC
ms.assetid: c69857e5-19ca-44aa-ae42-bc015be2b0f8
keywords:
- KSCATEGORY_VBICODEC 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_VBICODEC
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f51b03232f9ba15fb2407335ccc167d84073c8b7
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097237"
---
# <a name="kscategory_vbicodec"></a>KSCATEGORY_VBICODEC


KSCATEGORY_VBICODEC [设备接口类](./overview-of-device-interface-classes.md) 定义为 (KS) 功能类别的 [核心流式传输](../stream/streaming-minidrivers2.md) 间隔， (VBI) 编解码器设备。

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
<td align="left"><p>KSCATEGORY_VBICODEC</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{07DAD660-22F1-11D1-A9F4-00C04FBBDE8F}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_VBICODEC 的实例，以向操作系统指示设备支持 KSCATEGORY_VBICODEC 功能类别。

有关视频设备的常规信息，请参阅 [视频捕获设备](../stream/video-capture-devices.md)。

有关视频遮蔽的详细信息，请参阅 [从视频捕获设备流式传输数据](../stream/streaming-data-from-a-video-capture-device.md) 和 [VBI 类别](../stream/vbi-category.md)。

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


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

