---
title: KSCATEGORY_VBICODEC
description: KSCATEGORY_VBICODEC
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
ms.openlocfilehash: fbf62effe0404f0fcc6d555ab9e608c8c2cabfbc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832337"
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

## <a name="see-also"></a>请参阅


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

