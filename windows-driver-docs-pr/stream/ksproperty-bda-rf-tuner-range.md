---
title: KSPROPERTY\_BDA\_RF\_TUNER\_RANGE
description: 客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_范围来控制调谐器范围，也就是说，若要查找特定的载波频率的域。
ms.assetid: 2f2aa515-3f3c-419f-a817-0d597466ec85
keywords:
- KSPROPERTY_BDA_RF_TUNER_RANGE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_RF_TUNER_RANGE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e409cbd8b3785350a83e8422f59725adb88e30f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541323"
---
# <a name="kspropertybdarftunerrange"></a>KSPROPERTY\_BDA\_RF\_TUNER\_RANGE


客户端使用 KSPROPERTY\_BDA\_RF\_调谐器\_范围来控制调谐器范围，也就是说，若要查找特定的载波频率的域。

## <span id="ddk_ksproperty_bda_rf_tuner_range_ks"></span><span id="DDK_KSPROPERTY_BDA_RF_TUNER_RANGE_KS"></span>


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
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定调谐器节点的标识符。

属性值指定要设置的调谐器范围。

指定 KSPROPERTY\_BDA\_RF\_调谐器\_范围具有的属性：

-   BDA\_范围\_不\_设定 (− 1)，表示未设置调谐器范围。

-   BDA\_范围\_不\_定义 (0) 指示未定义调谐器范围。

某些调谐器控制多交换，它定义要查找特定的载波频率域等外部设备。 此属性设置调谐器范围到 − 1，这意味着对于特定的优化空间，不使用该调谐器范围，还是为特定于优化空间的值。

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
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






