---
title: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 分配
description: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 分配属性用于告知驱动程序何时为其侦听器数据分配和释放存储。
ms.assetid: 2e7256d0-578d-4b6e-aa5f-9e42e649523b
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0aec8c10d0d9c07ac9a68f5387e21786a165e61
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102542"
---
# <a name="ksproperty_directsound3dlistener_allocation"></a>KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 分配


KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 分配属性用于告知驱动程序何时为其侦听器数据分配和释放存储。 在创建侦听器时分配存储，并在删除侦听器时释放存储。 此属性还可用于查询驱动程序是否当前已分配侦听器数据。

## <span id="ddk_ksproperty_directsound3dlistener_allocation_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ALLOCATION_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">获取</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

操作数据) 的属性值 (为 BOOL 类型。 对于设置属性请求，此值指定驱动程序是否应为其侦听器数据分配或释放存储：

-   如果值为 **TRUE** ，则指示驱动程序为其侦听器数据分配存储空间。

-   如果值为 **FALSE** ，则通知驱动程序释放侦听器数据。

对于 get 属性请求，值为 **TRUE** 或 **FALSE** 指示驱动程序当前是否保留侦听器数据的存储分配。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ 分配属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

