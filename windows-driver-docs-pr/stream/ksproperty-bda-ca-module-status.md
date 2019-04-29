---
title: KSPROPERTY\_BDA\_CA\_模块\_状态
description: 客户端使用 KSPROPERTY\_BDA\_CA\_模块\_状态以确定与 ECM 映射节点关联的 CA 模块的状态。
ms.assetid: 4bd8a423-7a76-4702-a769-0de88fcc5772
keywords:
- KSPROPERTY_BDA_CA_MODULE_STATUS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_MODULE_STATUS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: eba1d9e571a7b816c3d134d383e60323b4aa016b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325249"
---
# <a name="kspropertybdacamodulestatus"></a>KSPROPERTY\_BDA\_CA\_模块\_状态


客户端使用 KSPROPERTY\_BDA\_CA\_模块\_状态以确定与 ECM 映射节点关联的 CA 模块的状态。

## <span id="ddk_ksproperty_bda_ca_module_status_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_MODULE_STATUS_KS"></span>


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

返回的值指定 CA 模块状态。

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


[**KSEVENT\_BDA\_CA\_模块\_状态\_已更改**](ksevent-bda-ca-module-status-changed.md)

[**KSP\_NODE**](https://msdn.microsoft.com/library/windows/hardware/ff566720)

 

 






