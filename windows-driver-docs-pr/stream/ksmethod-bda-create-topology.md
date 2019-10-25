---
title: KSMETHOD\_BDA\_创建\_拓扑
description: 客户端使用 KSMETHOD\_BDA\_创建\_拓扑，以便在第3环中创建拓扑结构，以在筛选器中反映已知的连接。
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
ms.openlocfilehash: 72a9609f50607d6922f8f06cef01c095b2494a63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842423"
---
# <a name="ksmethod_bda_create_topology"></a>KSMETHOD\_BDA\_创建\_拓扑


客户端使用 KSMETHOD\_BDA\_创建\_拓扑，以便在第3环中创建拓扑结构，以在筛选器中反映已知的连接。

## <span id="ddk_ksmethod_bda_create_topology_ks"></span><span id="DDK_KSMETHOD_BDA_CREATE_TOPOLOGY_KS"></span>


### <a name="span-idspecifying_this_methodspanspan-idspecifying_this_methodspanspan-idspecifying_this_methodspanspecifying-this-method"></a><span id="Specifying_This_Method"></span><span id="specifying_this_method"></span><span id="SPECIFYING_THIS_METHOD"></span>指定此方法

KSMETHOD，将**Flags**成员设置为 KSMETHOD\_键入\_WRITE。

### <a name="span-idmethod_dataspanspan-idmethod_dataspanspan-idmethod_dataspanmethod-data"></a><span id="Method_Data"></span><span id="method_data"></span><span id="METHOD_DATA"></span>方法数据

KSMULTIPLE\_项结构，它是拓扑信息列表的标头。

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


[**BdaMethodCreateTopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdamethodcreatetopology)

[**KSMETHOD**](https://docs.microsoft.com/previous-versions/ff563398(v=vs.85))

[**KSMULTIPLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)

 

 






