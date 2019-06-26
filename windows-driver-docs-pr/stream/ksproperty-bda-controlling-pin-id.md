---
title: KSPROPERTY\_BDA\_控制\_PIN\_ID
description: 客户端使用 KSPROPERTY\_BDA\_控制\_PIN\_要检索的控制 pin BDA 模板连接列表中的节点 ID。
ms.assetid: d40454a3-0938-4efb-8b06-06b599be8b20
keywords:
- KSPROPERTY_BDA_CONTROLLING_PIN_ID 流式处理媒体设备
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
ms.openlocfilehash: 341b8b200e8f9678b161a7989e236323874b39f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364883"
---
# <a name="kspropertybdacontrollingpinid"></a>KSPROPERTY\_BDA\_控制\_PIN\_ID


客户端使用 KSPROPERTY\_BDA\_控制\_PIN\_要检索的控制 pin BDA 模板连接列表中的节点 ID。

## <span id="ddk_ksproperty_bda_controlling_pin_id_ks"></span><span id="DDK_KSPROPERTY_BDA_CONTROLLING_PIN_ID_KS"></span>


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
<td><p>Filter</p></td>
<td><p>KSP_BDA_NODE_PIN</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的值指定控制 pin id。

节点相关联的筛选器，输入插针或输出插针中的一个 pin。 因为节点不具有其自己的文件句柄，则仅可以通过控制 pin 访问节点。 网络提供商可以使用此属性和 KSP\_BDA\_节点\_查询 BDA 模板连接列表中的每个节点的控制 pin 的 PIN 结构 (KSTOPOLOGY\_连接或 BDA\_模板\_连接数组)。

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
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**BdaPropertyGetControllingPinId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertygetcontrollingpinid)

[**BDA\_模板\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdatypes/ns-bdatypes-_bda_template_connection)

[**KSP\_BDA\_NODE\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ns-bdamedia-_ksp_bda_node_pin)

[**KSTOPOLOGY\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstopology_connection)

 

 






