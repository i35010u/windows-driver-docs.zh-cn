---
title: KSPROPERTY\_BDA\_信号\_质量
description: 客户端使用 KSPROPERTY\_BDA\_信号\_质量来确定从以百分比表示的信号已成功提取的数据量。
ms.assetid: 8967400d-3a10-475a-997a-d756837c3438
keywords:
- KSPROPERTY_BDA_SIGNAL_QUALITY 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SIGNAL_QUALITY
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b41a7533e37799f3f654b31e0ab562a8540168cb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361121"
---
# <a name="kspropertybdasignalquality"></a>KSPROPERTY\_BDA\_信号\_质量


客户端使用 KSPROPERTY\_BDA\_信号\_质量来确定从以百分比表示的信号已成功提取的数据量。

## <span id="ddk_ksproperty_bda_signal_quality_ks"></span><span id="DDK_KSPROPERTY_BDA_SIGNAL_QUALITY_KS"></span>


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
<td><p>Pin 或筛选器</p></td>
<td><p>KSP_NODE</p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

**NodeId** KSP 成员\_节点指定的控制节点的标识符，或设置为 − 1，以指定一个 pin。

返回的值指定从以百分比表示的信号中提取的数据。

解调节点通常报告信号质量，这是原始的数据量可能被提取信号中的表示形式。

通过检查水平同步未水平 （同步） 和垂直同步 （竖线） 的时间以及通过查看消隐 (HBlanking) 功能水平和垂直消隐功能 (VBlanking) 中包含的信息，则可以计算在模拟信号的情况下此百分比时间间隔。

在数字信号的情况下此百分比可通过检查数据包循环冗余检查 (CRC) 计算，并转发错误纠错 (FEC) 置信度值，如下所示：

-   100%是理想选择。

-   95%显示很少 （之举） 项目时呈现。

-   90%包含几个足够项目，就可以轻松地查看。

-   80%是最小级别，可以查看。

-   60%是最小级别出现数据服务，包括接收电子版收视指南 (EPG)，若要运行的情况。

-   20%指示解调器注意正确调制的信号存在但不能生成足够的数据很有用。

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

 

 






