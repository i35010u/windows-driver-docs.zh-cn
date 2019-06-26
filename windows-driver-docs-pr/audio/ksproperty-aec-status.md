---
title: KSPROPERTY\_AEC\_状态
description: KSPROPERTY\_AEC\_STATUS 属性用于监视 AEC 节点的状态 (KSNODETYPE\_声学\_ECHO\_取消)。 这是可选的 AEC 节点的属性。
ms.assetid: cd344367-1cb3-425a-8b22-300a85514e20
keywords:
- KSPROPERTY_AEC_STATUS 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AEC_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 403fc77222bac6d5de7c486af188bb73d9c90bb8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354422"
---
# <a name="kspropertyaecstatus"></a>KSPROPERTY\_AEC\_状态


KSPROPERTY\_AEC\_STATUS 属性用于监视 AEC 节点的状态 ([**KSNODETYPE\_声学\_ECHO\_取消**](ksnodetype-acoustic-echo-cancel.md)). 这是可选的 AEC 节点的属性。

## <span id="ddk_ksproperty_aec_status_ks"></span><span id="DDK_KSPROPERTY_AEC_STATUS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

类型为 ULONG 是属性值 （操作数据）。 这是可以将设置为一个或多个标志位左侧列中的下表中，标头文件 Ksmedia.h 中定义的按位 OR 的状态值。 相应 DSCFX\_AEC\_表的右侧列中显示从标头文件 Dsound.h 状态标志。 请参阅 Microsoft Windows SDK 文档，以了解有关这些标志。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">AEC 的状态标志</th>
<th align="left">ReplTest1</th>
<th align="left">DSCFX_AEC_STATUS 标志</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>AEC_STATUS_FD_HISTORY_UNINITIALIZED</p></td>
<td align="left"><p>0x0</p></td>
<td align="left"><p>DSCFX_AEC_STATUS_HISTORY_UNINITIALIZED</p></td>
</tr>
<tr class="even">
<td align="left"><p>AEC_STATUS_FD_HISTORY_CONTINUOUSLY_CONVERGED</p></td>
<td align="left"><p>0x1</p></td>
<td align="left"><p>DSCFX_AEC_STATUS_HISTORY_CONTINUOUSLY_CONVERGED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AEC_STATUS_FD_HISTORY_PREVIOUSLY_DIVERGED</p></td>
<td align="left"><p>0x2</p></td>
<td align="left"><p>DSCFX_AEC_STATUS_HISTORY_PREVIOUSLY_DIVERGED</p></td>
</tr>
<tr class="even">
<td align="left"><p>AEC_STATUS_FD_CURRENTLY_CONVERGED</p></td>
<td align="left"><p>0x8</p></td>
<td align="left"><p>DSCFX_AEC_STATUS_CURRENTLY_CONVERGED</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AEC\_状态属性请求返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

中的 AEC 状态标志的三个最低有效位 （请参阅上表） 表示 AEC 算法收敛历史的记录 (CH)。 CH 状态位可以由 Microsoft DirectSound 应用程序，用于确定是否算法已收敛，而且还是否它中聚合状态自其开始处理数据的时间。 具体取决于音频硬件，AEC 算法可能无法收敛，这种情况下生成的捕获缓冲区很可能包含从扬声器 echo。

当创建筛选器包含 AEC 节点或节点重置时，AEC 算法最初将三个 CH 状态位设置为零。 此设置来表示未初始化的状态的 AEC\_状态\_FD\_历史记录\_未初始化。

CH 状态 AEC 算法收敛后，切换到已聚合状态，AEC\_状态\_FD\_历史记录\_持续\_聚合。 如果 AEC 算法不断失去收敛，CH 状态切换到 diverged 状态，AEC\_状态\_FD\_历史记录\_以前\_DIVERGED。 尽管状态是最有可能从聚合状态切换为 diverged 状态，但它可能还切换直接从初始化状态到 diverged 状态。 CH 状态已切换到 diverged 状态后，它将保留，因为检测到之前的算法是重置或资源不足的状态。

当[AEC 系统筛选器](https://docs.microsoft.com/windows-hardware/drivers/audio/aec-system-filter)检测到资源不足的其四个插针，-任一个中的捕获、 捕获扩展、 呈现器中或呈现出-它将重置其内部状态，包括聚合历史记录。

请注意，第三个 CH 状态位的 2 位当前未使用。

除了使用 CH 状态位，作为应用程序可以监视实时聚合的状态检查 AEC\_状态\_FD\_当前\_聚合标志位。 如果设置此位，该算法是当前聚合。 暂时声学路径中发生更改时，该算法可能会丢失收敛。 实时聚合标志进行筛选，以防止这种瞬间损失不恰当地切换到 DSCFX CH 状态位\_AEC\_状态\_FD\_历史记录\_以前\_分离状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_ACOUSTIC\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)

 

 






