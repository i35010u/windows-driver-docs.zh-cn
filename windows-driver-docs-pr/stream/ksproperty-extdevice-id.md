---
title: KSPROPERTY\_EXTDEVICE\_ID
description: KSPROPERTY\_EXTDEVICE\_ID 属性检索外部设备通用化系统范围内的 Id。
ms.assetid: ff0f37f8-55a8-45b9-8cf1-81e2cc5ac3aa
keywords:
- KSPROPERTY_EXTDEVICE_ID 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_ID
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0992004c619088921974b2a7c4653b63b85f4939
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827029"
---
# <a name="ksproperty_extdevice_id"></a>KSPROPERTY\_EXTDEVICE\_ID


KSPROPERTY\_EXTDEVICE\_ID 属性检索外部设备通用化系统范围内的 Id。

## <span id="ddk_ksproperty_extdevice_id_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_ID_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>“获取”</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>DWORD 数组</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一个 DWORD 数组，用于指定外部设备的唯一节点 Id

<a name="remarks"></a>备注
-------

KSPROPERTY\_EXTDEVICE\_S 结构的**NodeUniqueID**成员指定了外部设备的唯一节点 Id。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTDEVICE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)

 

 






