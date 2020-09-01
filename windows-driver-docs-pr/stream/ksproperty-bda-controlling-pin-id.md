---
title: KSPROPERTY \_ BDA \_ 控制 \_ PIN \_ ID
description: 客户端使用 KSPROPERTY \_ BDA \_ 控制 \_ pin \_ ID 在 "BDA 模板连接" 列表中检索节点的控制 pin。
ms.assetid: d40454a3-0938-4efb-8b06-06b599be8b20
keywords:
- KSPROPERTY_BDA_CONTROLLING_PIN_ID 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CONTROLLING_PIN_ID
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddb3cba755f7fb6cf0f72baa5e4c65371bfeb3bb
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188145"
---
# <a name="ksproperty_bda_controlling_pin_id"></a>KSPROPERTY \_ BDA \_ 控制 \_ PIN \_ ID


客户端使用 KSPROPERTY \_ BDA \_ 控制 \_ pin \_ ID 在 "BDA 模板连接" 列表中检索节点的控制 pin。

## <span id="ddk_ksproperty_bda_controlling_pin_id_ks"></span><span id="DDK_KSPROPERTY_BDA_CONTROLLING_PIN_ID_KS"></span>


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
<th>获取</th>
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
<td><p>筛选器</p></td>
<td><p>KSP_BDA_NODE_PIN</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注解
-------

返回的值指定控制 pin ID。

节点与筛选器中的一个插针（输入插针或输出插针）相关联。 仅可通过控制 pin 访问节点，因为节点没有自己的文件句柄。 网络提供程序可以使用此属性和 KSP \_ BDA \_ 节点 \_ PIN 结构在 "BDA 模板连接列表" 中为每个节点查询控制 PIN (KSTOPOLOGY \_ 连接或 bda \_ 模板 \_ 连接数组) 。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**BdaPropertyGetControllingPinId**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertygetcontrollingpinid)

[**BDA \_ 模板 \_ 连接**](/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_template_connection)

[**KSP \_ BDA \_ 节点 \_ PIN**](/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-_ksp_bda_node_pin)

[**KSTOPOLOGY \_ 连接**](/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)

 

