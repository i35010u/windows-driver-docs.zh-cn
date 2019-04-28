---
title: KSPROPERTY\_连接\_状态
description: KSPROPERTY\_连接\_STATE 属性设置当前运行状态的 pin。
ms.assetid: f1a9e101-1398-4f16-bae9-f827e7d0c433
keywords:
- KSPROPERTY_CONNECTION_STATE 流式处理媒体设备
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
ms.openlocfilehash: 6ad42db96c218f457a53d7aef9a3272b98f81550
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338981"
---
# <a name="kspropertyconnectionstate"></a>KSPROPERTY\_连接\_状态


KSPROPERTY\_连接\_STATE 属性设置当前运行状态的 pin。

## <span id="ddk_ksproperty_connection_state_ks"></span><span id="DDK_KSPROPERTY_CONNECTION_STATE_KS"></span>


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
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>筛选器或 Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566856" data-raw-source="[&lt;strong&gt;KSSTATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566856)"><strong>KSSTATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性将返回以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KSSTATE_STOP</p></td>
<td><p>Pin 的初始状态。 没有数据实际上正在读取或写入。 在此状态下，pin 使用可能的资源量最少。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_ACQUIRE</p></td>
<td><p>Pin 获取读取或写入数据所需的资源。</p></td>
</tr>
<tr class="odd">
<td><p>KSSTATE_PAUSE</p></td>
<td><p>Pin 已准备好读取或写入数据，但暂时暂停数据传输。</p></td>
</tr>
<tr class="even">
<td><p>KSSTATE_RUN</p></td>
<td><p>状态从该 pin 可以实际读取或写入数据。</p></td>
</tr>
</tbody>
</table>

 

Pin 仅读取或写入的数据**KSSTATE\_运行**状态。 单个 pin 和 KS 筛选整个可能支持此属性。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSSTATE**](https://msdn.microsoft.com/library/windows/hardware/ff566856)

 

 






