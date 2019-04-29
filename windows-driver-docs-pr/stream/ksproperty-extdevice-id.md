---
title: KSPROPERTY\_EXTDEVICE\_ID
description: KSPROPERTY\_EXTDEVICE\_ID 属性检索外部设备的通用的系统范围 id。
ms.assetid: ff0f37f8-55a8-45b9-8cf1-81e2cc5ac3aa
keywords:
- KSPROPERTY_EXTDEVICE_ID 流式处理媒体设备
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
ms.openlocfilehash: 9c0cdefc40de4f831240723d0ec68528cad14fd0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373431"
---
# <a name="kspropertyextdeviceid"></a>KSPROPERTY\_EXTDEVICE\_ID


KSPROPERTY\_EXTDEVICE\_ID 属性检索外部设备的通用的系统范围 id。

## <span id="ddk_ksproperty_extdevice_id_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_ID_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

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
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>设备</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565156" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565156)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p>双字节数组</p></td>
</tr>
</tbody>
</table>

 

（操作数据） 的属性值是双字节数组，它指定外部设备的唯一节点 Id

<a name="remarks"></a>备注
-------

**NodeUniqueID** KSPROPERTY 成员\_EXTDEVICE\_S 结构指定外部设备的唯一节点 id。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_EXTDEVICE\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565156)

 

 






