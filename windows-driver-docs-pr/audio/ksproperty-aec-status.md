---
title: KSPROPERTY\_AEC\_状态
description: KSPROPERTY\_AEC\_STATUS 属性用于监视 AEC 节点的状态（KSNODETYPE\_声音\_ECHO\_CANCEL）。 这是 AEC 节点的一个可选属性。
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
ms.openlocfilehash: e295238892636fd1d4db7ef6e7ae6bd3d0b99b0a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833070"
---
# <a name="ksproperty_aec_status"></a>KSPROPERTY\_AEC\_状态


KSPROPERTY\_AEC\_STATUS 属性用于监视 AEC 节点的状态（[**KSNODETYPE\_声音\_ECHO\_CANCEL**](ksnodetype-acoustic-echo-cancel.md)）。 这是 AEC 节点的一个可选属性。

## <span id="ddk_ksproperty_aec_status_ks"></span><span id="DDK_KSPROPERTY_AEC_STATUS_KS"></span>


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
<th align="left">“获取”</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>“是”</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>大头针</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）的类型为 ULONG。 这是一个状态值，可以设置为下表左侧列中的一个或多个标志位的按位 "或" （在头文件 Ksmedia 中定义）。 标头文件 Dsound 中的相应 DSCFX\_AEC\_状态标志显示在表的右列中。 有关这些标志的信息，请参阅 Microsoft Windows SDK 文档。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">AEC 状态标志</th>
<th align="left">Value</th>
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

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_AEC\_STATUS 属性请求返回状态\_SUCCESS，以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

AEC 状态标志中的三个最小有效位（请参阅上表）表示 AEC 算法的聚合历史记录（CH）。 Microsoft DirectSound 应用程序可以使用 CH 状态位来确定算法是否已聚合，以及自开始处理数据后它是否保持收敛状态。 根据音频硬件，AEC 算法可能无法收敛，在这种情况下，生成的捕获缓冲区可能会包含来自扬声器的回显。

当创建包含 AEC 节点的筛选器或重置节点时，AEC 算法最初将三个 CH 状态位设置为零。 此设置表示未初始化状态\_状态\_FD\_历史记录\_未初始化。

在 AEC 算法聚合后，CH 状态切换到聚合状态，AEC\_状态\_FD\_历史记录\_持续\_聚合。 如果 AEC 算法丢失收敛，则 CH 状态将切换到分离状态，AEC\_状态\_FD\_历史记录\_之前\_的分离。 尽管状态最可能是从聚合状态切换到分离状态，但它也可能会直接从未初始化状态切换到分离状态。 在 CH 状态切换到 "分离" 状态后，它将保持该状态，直到检测到算法或检测到 "不足"。

当[AEC 系统筛选器](https://docs.microsoft.com/windows-hardware/drivers/audio/aec-system-filter)检测到其四个 pin 中的任何一种，即在中捕获、捕获、呈现或呈现出来时，它将重置其内部状态，包括聚合历史记录。

请注意，当前不使用三个 CH 状态位的第2位。

作为使用 CH 状态位的替代方法，应用程序可以通过检查 AEC\_状态\_FD\_当前\_聚合标志位来监视实时汇聚状态。 如果设置了此位，则算法当前已聚合。 当声音路径发生变化时，该算法可能会暂时失去收敛。 筛选实时聚合标志以防止此类暂时损失将 CH 状态位切换到 DSCFX\_AEC\_状态\_FD\_历史记录\_之前\_分离状态。

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
<td align="left">Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_声音\_回音\_取消**](ksnodetype-acoustic-echo-cancel.md)

 

 






