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
ms.openlocfilehash: 6477b7e7c12fbcd1a5f1f16840d46ec386935358
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385541"
---
# <a name="kscategoryvbicodec"></a>KSCATEGORY_VBICODEC


KSCATEGORY_VBICODEC[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 功能的视频的遮蔽间隔 (VBI) 编解码器设备类别。

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

KS 设备的驱动程序注册 KSCATEGORY_VBICODEC 向操作系统指示设备支持 KSCATEGORY_VBICODEC 功能分类的实例。

有关视频设备的常规信息，请参阅[视频捕获设备](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-devices)。

有关视频消隐功能的详细信息，请参阅[流式处理视频捕获设备中的数据](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-data-from-a-video-capture-device)并[VBI 类别](https://docs.microsoft.com/windows-hardware/drivers/stream/vbi-category)。

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
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSCATEGORY_VIDEO**](kscategory-video.md)

 

 






