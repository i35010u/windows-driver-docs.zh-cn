---
title: KSCATEGORY_VIDEO
description: KSCATEGORY_VIDEO
ms.assetid: cdcdb22b-3969-4c58-a8ce-a9d0b4b64e3b
keywords:
- KSCATEGORY_VIDEO 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_VIDEO
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bdac331cfd2a3d27f36e60346bfa515bff1f880b
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097239"
---
# <a name="kscategory_video"></a>KSCATEGORY_VIDEO


为视频设备的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_VIDEO[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_VIDEO</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{6994AD05-93EF-11D0-A3CC-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

适用于 KS 视频设备的驱动程序将 KSCATEGORY_VIDEO 的实例注册，以向操作系统指示设备支持 KSCATEGORY_VIDEO 功能类别。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 WDK 的*src/swtuner/algtuner*目录中的软件调谐器示例附带的*Bdan* inf 文件。

有关此功能类别的详细信息，请参阅 [提供 UVC INF 文件](../stream/providing-a-uvc-inf-file.md)。

有关视频设备的常规信息，请参阅 [视频捕获设备](../stream/video-capture-devices.md)。

有关视频设备的其他设备接口类的信息，请参阅 [**KSCATEGORY_TVAUDIO**](kscategory-tvaudio.md) 和 [**KSCATEGORY_TVTUNER**](kscategory-tvtuner.md)。

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


[**KSCATEGORY_TVAUDIO**](kscategory-tvaudio.md)

[**KSCATEGORY_TVTUNER**](kscategory-tvtuner.md)

 

