---
title: KSCATEGORY_INTERFACETRANSFORM
description: KSCATEGORY_INTERFACETRANSFORM
ms.assetid: a33b5de9-6b51-41a6-bb06-392e1438f0cc
keywords:
- KSCATEGORY_INTERFACETRANSFORM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- KSCATEGORY_INTERFACETRANSFORM
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d1bbca65c595a0157428ad7be6dce0b2e2decf2d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383748"
---
# <a name="kscategoryinterfacetransform"></a>KSCATEGORY_INTERFACETRANSFORM


KSCATEGORY_INTERFACETRANSFORM[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)为定义[内核流式处理](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 转换的设备接口的功能类别。

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
<td align="left"><p>KSCATEGORY_INTERFACETRANSFORM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{CF1DDA2D-9743-11D0-A3EE-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 设备的驱动程序注册 KSCATEGORY_INTERFACETRANSFORM 向操作系统指示设备支持 KSCATEGORY_INTERFACETRANSFORM 功能分类的实例。

KSCATEGORY_INTERFACETRANSFORM 功能类别是之一[ **KSPROPERTY_TOPOLOGY_CATEGORIES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)功能类别。

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

 

 






