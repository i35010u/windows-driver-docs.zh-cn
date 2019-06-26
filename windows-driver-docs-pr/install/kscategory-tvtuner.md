---
title: KSCATEGORY_TVTUNER
description: KSCATEGORY_TVTUNER
ms.assetid: 44d9d407-a94c-40de-b749-af50bc5718f4
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
ms.openlocfilehash: 3374f175c2d5fe9e14222fd41ffd59a91e2f9d7b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385544"
---
# <a name="kscategorytvtuner"></a>KSCATEGORY_TVTUNER


KSCATEGORY_TVTUNER[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)电视调谐器设备 (KS) 功能类别。

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

KS 设备的驱动程序注册 KSCATEGORY_TVTUNER 向操作系统指示设备支持 KSCATEGORY_TVTUNER 功能分类的实例。

有关如何在一个 INF 文件中注册此功能的类别的示例，请参阅*Bdan.inf* INF 文件，包括中的软件调谐器示例*src/swtuner/algtuner* WDK 的目录。

视频设备有关的信息，请参阅[视频捕获设备](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-devices)，[筛选器关系图示例](https://docs.microsoft.com/windows-hardware/drivers/stream/filter-graph-examples)，并[编码器设备](https://docs.microsoft.com/windows-hardware/drivers/stream/encoder-devices)。

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


[**KSCATEGORY_TVAUDIO**](kscategory-tvaudio.md)

 

 






