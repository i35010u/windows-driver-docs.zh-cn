---
title: KSMETHOD \_ BDA \_ CREATE \_ 拓扑
description: 客户端使用 KSMETHOD \_ BDA \_ create \_ 拓扑在环3中创建一个在筛选器中反映已知连接的拓扑结构。
ms.assetid: 3f34c7cc-d711-478b-a017-ad2c46545a9b
keywords:
- KSMETHOD_BDA_CREATE_TOPOLOGY 流媒体设备
topic_type:
- apiref
api_name:
- KSMETHOD_BDA_CREATE_TOPOLOGY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63bc719a72d8495ac8d4b6b9820efbb440fa5422
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192177"
---
# <a name="ksmethod_bda_create_topology"></a>KSMETHOD \_ BDA \_ CREATE \_ 拓扑


客户端使用 KSMETHOD \_ BDA \_ create \_ 拓扑在环3中创建一个在筛选器中反映已知连接的拓扑结构。

## <span id="ddk_ksmethod_bda_create_topology_ks"></span><span id="DDK_KSMETHOD_BDA_CREATE_TOPOLOGY_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

KSMETHOD，其 **Flags** 成员设置为 KSMETHOD \_ 类型 \_ WRITE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

KSMULTIPLE \_ 项结构，它是拓扑信息列表的标头。

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
<td>Bdamedia (包含 Bdamedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**BdaMethodCreateTopology**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethodcreatetopology)

[**KSMETHOD**](/previous-versions/ff563398(v=vs.85))

[**KSMULTIPLE \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

