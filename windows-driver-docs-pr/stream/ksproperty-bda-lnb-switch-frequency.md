---
title: KSPROPERTY\_BDA\_LNB\_SWITCH\_FREQUENCY
description: 客户端使用 KSPROPERTY\_BDA\_LNB\_切换\_通知 RF 调谐器节点有关的传入 RF 信号的调谐器应该通知低干扰块 (LNB) 设备，若要从切换的频率的频率使用低带本地震荡频率 (LOF) 到使用高外 LOF 或执行相反时 LNB 转移 RF 信号的频率。
ms.assetid: a448bad1-40dc-4596-bc18-9522144e33a7
keywords:
- KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d93fbc8e83491bae5d94a14d1d4ef61adb0150ad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376665"
---
# <a name="kspropertybdalnbswitchfrequency"></a>KSPROPERTY\_BDA\_LNB\_SWITCH\_FREQUENCY


客户端使用 KSPROPERTY\_BDA\_LNB\_切换\_通知 RF 调谐器节点有关的传入 RF 信号的调谐器应该通知低干扰块 (LNB) 设备，若要从切换的频率的频率使用低带本地震荡频率 (LOF) 到使用高外 LOF 或执行相反时 LNB 转移 RF 信号的频率。

## <span id="ddk_ksproperty_bda_lnb_switch_frequency_ks"></span><span id="DDK_KSPROPERTY_BDA_LNB_SWITCH_FREQUENCY_KS"></span>


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

**NodeId** KSP 成员\_节点指定 RF 调谐器节点的标识符。

属性值指定 LNB 应切换使用低外的 LOF 使用高外 LOF 传入 RF 信号的频率。

如果客户端发送 KSPROPERTY\_BDA\_RF\_调谐器\_频率请求来优化对特定频率和此频率 RF 调谐器是大于或等于指定使用 KSPROPERTY 的切换频率\_BDA\_LNB\_切换\_频率，然后 RF 调谐器应将命令发送到 LNB 切换到高外 LOF。 RF 调谐器然后应该会 LNB 设备由高外 LOF 量，使用 KSPROPERTY 指定将传入的 RF 信号的频率\_BDA\_LNB\_LOF\_高\_外。

同样，如果客户端发送 KSPROPERTY\_BDA\_RF\_调谐器\_频率请求来优化对特定频率和此频率 RF 调谐器小于交换机频率，则应发送 RF 调谐器若要切换到低外 LOF 到 LNB 命令。 RF 调谐器然后应该会 LNB 设备由低外 LOF 量，使用 KSPROPERTY 指定将传入的 RF 信号的频率\_BDA\_LNB\_LOF\_低\_外。

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


[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

[**KSPROPERTY\_BDA\_LNB\_LOF\_HIGH\_BAND**](ksproperty-bda-lnb-lof-high-band.md)

[**KSPROPERTY\_BDA\_LNB\_LOF\_LOW\_BAND**](ksproperty-bda-lnb-lof-low-band.md)

[**KSPROPERTY\_BDA\_RF\_调谐器\_频率**](ksproperty-bda-rf-tuner-frequency.md)

 

 






