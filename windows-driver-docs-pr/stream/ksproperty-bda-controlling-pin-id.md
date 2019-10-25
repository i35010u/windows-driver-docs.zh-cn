---
title: KSPROPERTY\_BDA\_控制\_PIN\_ID
description: 客户端使用 KSPROPERTY\_BDA\_控制\_PIN\_ID，以在 "BDA 模板连接" 列表中检索节点的控制 PIN。
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
ms.openlocfilehash: ecd8523aac5f65d37d29a0f5fc3167ea684f5673
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842149"
---
# <a name="ksproperty_bda_controlling_pin_id"></a>KSPROPERTY\_BDA\_控制\_PIN\_ID


客户端使用 KSPROPERTY\_BDA\_控制\_PIN\_ID，以在 "BDA 模板连接" 列表中检索节点的控制 PIN。

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
<td><p>Filter</p></td>
<td><p>KSP_BDA_NODE_PIN</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的值指定控制 pin ID。

节点与筛选器中的一个插针（输入插针或输出插针）相关联。 仅可通过控制 pin 访问节点，因为节点没有自己的文件句柄。 网络提供程序可以使用此属性和 KSP\_BDA\_NODE\_PIN 结构，以便在 "BDA 模板连接" 列表中查询每个节点的控制 PIN （KSTOPOLOGY\_连接或 BDA\_模板\_连接数组）。

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
<td>Bdamedia （包括 Bdamedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**BdaPropertyGetControllingPinId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdapropertygetcontrollingpinid)

[**BDA\_模板\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdatypes/ns-bdatypes-_bda_template_connection)

[**KSP\_BDA\_NODE\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-_ksp_bda_node_pin)

[**KSTOPOLOGY\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kstopology_connection)

 

 






