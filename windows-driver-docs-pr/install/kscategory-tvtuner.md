---
title: KSCATEGORY_TVTUNER
description: KSCATEGORY_TVTUNER
keywords:
- KSCATEGORY_TVTUNER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_TVTUNER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6fdd0aa72c35f23927f25a891e317cabed628f90
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832341"
---
# <a name="kscategory_tvtuner"></a>KSCATEGORY_TVTUNER


为电视调谐器设备的[内核流式处理](../stream/streaming-minidrivers2.md) (KS) 功能类别定义 KSCATEGORY_TVTUNER[设备接口类](./overview-of-device-interface-classes.md)。

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
<td align="left"><p>KSCATEGORY_TVTUNER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{A799A800-A46D-11D0-A18C-00A02401DCD4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序将注册 KSCATEGORY_TVTUNER 的实例，以向操作系统指示设备支持 KSCATEGORY_TVTUNER 功能类别。

有关如何在 INF 文件中注册此功能类别的示例，请参阅 WDK 的 *src/swtuner/algtuner* 目录中的软件调谐器示例附带的 *Bdan* inf 文件。

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

## <a name="see-also"></a>请参阅


[**KSCATEGORY_TVAUDIO**](kscategory-tvaudio.md)

 

