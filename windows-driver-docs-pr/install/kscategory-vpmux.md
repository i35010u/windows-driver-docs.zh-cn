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
ms.openlocfilehash: c8b835c7274b31514326abc311284ebf12911ca9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385540"
---
# <a name="kscategoryvpmux"></a>KSCATEGORY_VPMUX


KSCATEGORY_VPMUX[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 支持视频的多路复用的功能类别。

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

KS 设备的驱动程序注册 KSCATEGORY_VPMUX 向操作系统指示设备支持 KSCATEGORY_VPMUX 功能分类的实例。

有关视频设备的常规信息，请参阅[视频捕获设备](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-devices)。

有关视频设备的设备接口类的信息，请参阅[ **KSCATEGORY_VIDEO**](kscategory-video.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

 






