---
title: KSPROPERTY\_连接\_状态
description: KSPROPERTY\_连接\_状态属性设置 pin 的当前运行状态。
ms.assetid: f1a9e101-1398-4f16-bae9-f827e7d0c433
keywords:
- KSPROPERTY_CONNECTION_STATE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CONNECTION_STATE
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 187e78a7790a128fa975bacc15ad5a552c3660f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826779"
---
# <a name="ksproperty_connection_state"></a>KSPROPERTY\_连接\_状态


KSPROPERTY\_连接\_状态属性设置 pin 的当前运行状态。

## <span id="ddk_ksproperty_connection_state_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_STATE_KS"></span>


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
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>筛选器或固定</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate" data-raw-source="[&lt;strong&gt;KSSTATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)"><strong>KSSTATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSSTATE_STOP</p></td>
<td><p>Pin 的初始状态。 实际上没有读取或写入数据。 在此状态下，pin 将使用尽可能少的资源。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_ACQUIRE</p></td>
<td><p>Pin 正在获取读取或写入数据所需的资源。</p></td>
</tr>
<tr class="odd">
<td><p>KSSTATE_PAUSE</p></td>
<td><p>Pin 已准备好读取或写入数据，但数据传输已暂时暂停。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_RUN</p></td>
<td><p>Pin 可以从其实际读取或写入数据的状态。</p></td>
</tr>
</tbody>
</table>

 

Pin 仅在**KSSTATE\_运行**状态中读取或写入数据。 单个 pin 和 KS 筛选器整体都可能支持此属性。

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
<td>Ks （包含 Ks）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)

 

 






