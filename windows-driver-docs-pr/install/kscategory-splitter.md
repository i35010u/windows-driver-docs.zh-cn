---
title: KSCATEGORY_SPLITTER
description: KSCATEGORY_SPLITTER
ms.assetid: 056b6bc0-5566-4498-959d-dbc9725aa03e
keywords:
- KSCATEGORY_SPLITTER 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_SPLITTER
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c1c0ec5833c3af47f354307de44466fbff619e87
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366699"
---
# <a name="kscategorysplitter"></a>KSCATEGORY_SPLITTER


KSCATEGORY_SPLITTER[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 功能类别将拆分数据流。

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
<td align="left"><p>KSCATEGORY_SPLITTER</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{0A4252A0-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 音频适配器设备驱动程序注册 KSCATEGORY_SPLITTER 向操作系统指示设备支持 KSCATEGORY_SPLITTER 功能分类的实例。

KSCATEGORY_SPLITTER 功能类别是之一[ **KSPROPERTY_TOPOLOGY_CATEGORIES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)功能类别。

有关拆分条中的常规信息，请参阅[AVStream 拆分条](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-splitters)。

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


[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)

 

 






