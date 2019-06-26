---
title: KSCATEGORY_DATADECOMPRESSOR
description: KSCATEGORY_DATADECOMPRESSOR
ms.assetid: 260906fc-fdd5-487f-9f45-db6ca4591233
keywords:
- KSCATEGORY_DATADECOMPRESSOR 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_DATADECOMPRESSOR
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8f48389862715402ab944f96cd5efff469440c20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385900"
---
# <a name="kscategorydatadecompressor"></a>KSCATEGORY_DATADECOMPRESSOR


KSCATEGORY_DATADECOMPRESSOR[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)解压缩的数据流的 (KS) 功能类别。

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
<td align="left"><p>KSCATEGORY_DATADECOMPRESSOR</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{2721AE20-7E70-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_DATADECOMPRESSOR 向操作系统指示设备支持 KSCATEGORY_DATADECOMPRESSOR 功能分类的实例。

KSCATEGORY_DATADECOMPRESSOR 功能类别是之一[ **KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)。

有关为压缩数据流的 KS 功能类别定义的设备接口类的信息，请参阅[ **KSCATEGORY_DATACOMPRESSOR**](kscategory-datacompressor.md)。

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


[**KSCATEGORY_DATACOMPRESSOR**](kscategory-datacompressor.md)

[**KSPROPERTY_TOPOLOGY_CATEGORIES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)

 

 






