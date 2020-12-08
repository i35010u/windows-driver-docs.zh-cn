---
title: KSCATEGORY_VPMUX
description: KSCATEGORY_VPMUX
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
ms.openlocfilehash: 967a151dda56fa955bf9745839e2008e9d1df9da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832325"
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

## <a name="see-also"></a>请参阅


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

