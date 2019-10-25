---
title: KSEVENT\_调谐器\_启动\_扫描
description: KSEVENT\_调谐器\_启动\_扫描事件请求驱动程序启动扫描操作，并在驱动程序的相关优化设备完成扫描操作时通知用户模式客户端。
ms.assetid: 63f6917e-30d2-4734-92fa-49a4291efafd
keywords:
- KSEVENT_TUNER_INITIATE_SCAN 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_TUNER_INITIATE_SCAN
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83ab636034238f8f3a1d5616767a13910bb3b8b7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844922"
---
# <a name="ksevent_tuner_initiate_scan"></a>KSEVENT\_调谐器\_启动\_扫描


KSEVENT\_调谐器\_启动\_扫描事件请求驱动程序启动扫描操作，并在驱动程序的相关优化设备完成扫描操作时通知用户模式客户端。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th>事件描述符类型</th>
<th>事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无</p></td>
<td><p>“是”</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)"><strong>KSEVENT_TUNER_INITIATE_SCAN_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

每个扫描请求应为非阻塞。 也就是说，驱动程序在返回 control 之前不应等待扫描操作完成。 事实上，驱动程序应使用单独的线程来执行扫描操作。

尽管 KSEVENT\_调谐器\_启动\_SCAN 事件与[**KSPROPERTY\_调谐器无关\_频率**](ksproperty-tuner-frequency.md)、KSEVENT\_调谐器\_启动\_扫描对应于**KS\_调谐器\_优化**在 KSPROPERTY\_调谐器的**TuningFlags**成员中\_精确的调谐标志[ **\_FREQUENCY\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s)结构。 这意味着扫描始终会尝试确定下一通道的准确频率。 此外，优化设备遵循的优化策略由驱动程序（KS\_调谐器\_策略控制\_驱动程序\_从 KSPROPERTY\_的**战略**成员\_[ **\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s)结构）。 即使使用不同的标志和策略来控制**KSPROPERTY\_调谐器\_频率**，也始终遵循这些固定标志和策略。

换而言之，KSTUNER\_优化\_标志和 KSTUNER\_策略值不会影响 KSEVENT\_调谐器\_启动\_扫描的行为。

***<em>完成和状态</em>***

扫描状态属性[**KSPROPERTY\_调谐器\_scan\_状态**](ksproperty-tuner-scan-status.md)提供有关信号锁定的当前频率和状态的信息。 应用程序从 KSPROPERTY\_调谐器\_SCAN\_STATUS 属性查询锁定状态。 该应用程序还会在[**KSPROPERTY\_调谐器\_标准\_模式**](ksproperty-tuner-standard-mode.md)属性中查询有关自动信号标准检测的信息。 如果在所请求的范围内找不到信号，则 KSPROPERTY\_调谐器\_SCAN\_STATUS 属性返回 KSPROPERTY\_调谐器的**LockStatus**成员中的**调谐器\_LockType\_无**值[ **\_扫描\_状态\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)结构。 如果优化设备可以通过信号自动检测调谐器标准，并且发现备用标准中有信号，则优化设备本身可以处理对[**KSPROPERTY\_调谐器**](ksproperty-tuner-standard.md)的任何请求\_标准属性。 优化设备可能无法超出分阶段锁（PLL）锁，并且它可能会指定标准未知。 或者，调谐设备可能会自动调整到不同的信号标准。 此外，优化设备甚至可以获取该信号标准的完全锁定，并确定备用的标准。 在频率范围内有多个信号标准时，可能会出现这种情况。

***<em>边界条件</em>***

如果驱动程序发现通道的中心频率在应用程序提供的范围之外，则驱动程序必须忽略该信号，并移到下一个信号;驱动程序不能在提供的范围内返回最佳的近似值。 当应用程序尝试编译通道列表时，驱动程序必须转到下一信号，以避免通道的重复计数。

由于同样的原因，应用程序必须将查询范围移到预期的通道带宽一半（约 6/2 = 3MHz 用于模拟和数字电视），以确保在硬件遇到硬件无法解码。 在这种情况下，驱动程序很难避免对某些通道进行双重计数。

***<em>多标准 Spectra</em>***

只要发现新的通道或信号，就必须完成扫描操作。 然后，该驱动程序通过[**KSPROPERTY\_调谐器\_scan\_status**](ksproperty-tuner-scan-status.md)属性返回扫描状态。 即使驱动程序确定新找到的通道与以前应用的标准不匹配，只要找到新通道，就必须完成扫描。 应用程序必须处理新的通道信息，并且必须重新提交扫描请求以查找信号标准相同的另一个通道。

## <a name="see-also"></a>另请参阅


[**KSEVENT\_调谐器\_启动\_扫描\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)

[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**KSPROPERTY\_调谐器\_扫描\_状态**](ksproperty-tuner-scan-status.md)

[**KSPROPERTY\_调谐器\_扫描\_CAP**](ksproperty-tuner-scan-caps.md)

[**KSPROPERTY\_调谐器\_标准**](ksproperty-tuner-standard.md)

[**KSPROPERTY\_调谐器\_标准\_模式**](ksproperty-tuner-standard-mode.md)

 

 






