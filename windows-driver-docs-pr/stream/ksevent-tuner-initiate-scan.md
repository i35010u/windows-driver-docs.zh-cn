---
title: KSEVENT\_调谐器\_启动\_扫描
description: KSEVENT\_调谐器\_启动\_扫描事件请求驱动程序启动扫描操作，并通知用户模式下客户端时，驱动程序的关联优化设备完成扫描操作。
ms.assetid: 63f6917e-30d2-4734-92fa-49a4291efafd
keywords:
- KSEVENT_TUNER_INITIATE_SCAN 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_TUNER_INITIATE_SCAN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff8630acc99a3a65d13de67cb18ad7c26fe170da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545659"
---
# <a name="kseventtunerinitiatescan"></a>KSEVENT\_调谐器\_启动\_扫描


KSEVENT\_调谐器\_启动\_扫描事件请求驱动程序启动扫描操作，并通知用户模式下客户端时，驱动程序的关联优化设备完成扫描操作。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th>事件描述符类型</th>
<th>事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561901" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561901)"><strong>KSEVENT_TUNER_INITIATE_SCAN_S</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561750" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561750)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

扫描的每个请求应为非阻塞。 也就是说，该驱动程序不应等待扫描操作完成之前会将控件返回。 实际上，该驱动程序应使用单独的线程来执行扫描操作。

尽管 KSEVENT\_调谐器\_启动\_扫描事件是独立于[ **KSPROPERTY\_调谐器\_频率**](ksproperty-tuner-frequency.md)，KSEVENT\_调谐器\_启动\_扫描对应于**KS\_调谐器\_优化\_EXACT**中的优化标志**TuningFlags**的成员[ **KSPROPERTY\_调谐器\_频率\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565839)结构。 这意味着，扫描始终会尝试确定确切的频率的下一个通道。 此外，优化设备遵循的优化策略控制驱动程序 (KS\_调谐器\_策略\_驱动程序\_优化从**策略**成员[ **KSPROPERTY\_调谐器\_模式\_CAPS\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565872)结构)。 即使另一标记和策略是用于控制始终遵循这些固定的标志和战略**KSPROPERTY\_调谐器\_频率**。

换而言之，KSTUNER\_TUNING\_标志和 KSTUNER\_策略值不会影响 KSEVENT 行为\_调谐器\_启动\_扫描。

***<em>完成和状态</em>***

扫描状态属性[ **KSPROPERTY\_调谐器\_扫描\_状态**](ksproperty-tuner-scan-status.md)提供有关当前的频率和信号锁的状态信息。 应用程序在查询的锁定状态从 KSPROPERTY\_调谐器\_扫描\_STATUS 属性。 应用程序也会询问[ **KSPROPERTY\_调谐器\_标准\_模式**](ksproperty-tuner-standard-mode.md)属性以获取有关自动信号标准检测的信息。 如果没有信号找在请求范围内，KSPROPERTY\_调谐器\_扫描\_状态属性将返回**调谐器\_LockType\_无**中的值**LockStatus**的成员[ **KSPROPERTY\_调谐器\_扫描\_状态\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565898)结构。 如果优化设备可以自动检测信号的调谐器标准，信号备用标准中的未找到，优化设备本身可以处理任何请求[ **KSPROPERTY\_调谐器\_标准**](ksproperty-tuner-standard.md)属性。 优化设备程序可能无法继续超出分阶段-锁定-循环 (PLL) 锁，但它可能会指定标准未知。 或者，优化设备可能会自动调整到不同的信号标准。 此外，优化设备甚至可能会获取该信号标准的完整锁并确定备用标准。 频率范围中有多个信号标准，可能会出现这种情况。

***<em>边界条件</em>***

如果驱动程序将查找一个通道的中心频率是应用程序提供了范围之外，驱动程序必须忽略该信号，并转到下一个信号;该驱动程序不能返回提供的范围内的最可能近似。 该驱动程序必须将移动到下一个信号，以避免重复计算的通道时应用程序尝试编译通道列表。

出于相同原因，应用程序必须移动的范围查询的一半的预期的通道带宽 (大约 6/2 = 3 的模拟和数字电视 MHz) 以确保通道不双计数尤其是当硬件遇到信号的硬件不能进行解码。 在此情况下，驱动程序必须避免重复计算某些通道的难度。

***<em>多标准 Spectra</em>***

每当一个新通道，必须完成扫描操作或信号找到。 然后，该驱动程序返回通过扫描状态[ **KSPROPERTY\_调谐器\_扫描\_状态**](ksproperty-tuner-scan-status.md)属性。 只要新的通道找到即使该驱动程序确定的最新找到的通道与以前应用的标准不匹配，则必须完成扫描。 应用程序必须处理新的通道信息，必须重新提交扫描请求以查找具有相同的信号的另一个通道标准。

## <a name="see-also"></a>另请参阅


[**KSEVENT\_调谐器\_启动\_扫描\_S**](https://msdn.microsoft.com/library/windows/hardware/ff561901)

[**KSEVENTDATA**](https://msdn.microsoft.com/library/windows/hardware/ff561750)

[**KSPROPERTY\_调谐器\_扫描\_状态**](ksproperty-tuner-scan-status.md)

[**KSPROPERTY\_调谐器\_扫描\_CAP**](ksproperty-tuner-scan-caps.md)

[**KSPROPERTY\_调谐器\_标准**](ksproperty-tuner-standard.md)

[**KSPROPERTY\_调谐器\_标准\_模式**](ksproperty-tuner-standard-mode.md)

 

 






