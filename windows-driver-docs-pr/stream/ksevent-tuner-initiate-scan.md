---
title: KSEVENT \_ 调谐器 \_ 启动 \_ 扫描
description: KSEVENT \_ 调谐器 \_ 启动 \_ 扫描事件请求，驱动程序启动扫描操作，并在驱动程序的相关优化设备完成扫描操作时通知用户模式客户端。
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
ms.openlocfilehash: a33ac88534cc0a703b19d78caab3a355233087d5
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106006"
---
# <a name="ksevent_tuner_initiate_scan"></a>KSEVENT \_ 调谐器 \_ 启动 \_ 扫描


KSEVENT \_ 调谐器 \_ 启动 \_ 扫描事件请求，驱动程序启动扫描操作，并在驱动程序的相关优化设备完成扫描操作时通知用户模式客户端。

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
<th>获取</th>
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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s" data-raw-source="[&lt;strong&gt;KSEVENT_TUNER_INITIATE_SCAN_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)"><strong>KSEVENT_TUNER_INITIATE_SCAN_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

每个扫描请求应为非阻塞。 也就是说，驱动程序在返回 control 之前不应等待扫描操作完成。 事实上，驱动程序应使用单独的线程来执行扫描操作。

尽管 KSEVENT \_ 调谐器 \_ 启动 \_ 扫描事件独立于[**KSPROPERTY \_ 调谐器 \_ 频率**](ksproperty-tuner-frequency.md)，但 KSEVENT \_ 调谐器 \_ 启动扫描对应于 \_ [** \_ 调谐器 \_ frequency \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_frequency_s)结构的**TuningFlags**成员中的**KS \_ 调谐器 \_ 优化 \_ 精确**优化标志。 这意味着扫描始终会尝试确定下一通道的准确频率。 此外，优化设备遵循的优化策略由驱动程序 (KS \_ 调谐器 \_ 策略 \_ 驱动程序的) 的 \_ **策略** 成员 [** \_ \_ \_ \_ **](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_caps_s) 进行控制。 即使使用不同的标志和策略来控制 **KSPROPERTY \_ 调谐器 \_ 频率**，这些固定标志和策略也始终遵循。

换句话说，KSTUNER \_ 调谐 \_ 标志和 KSTUNER \_ 策略值不会影响 KSEVENT \_ 调谐器 \_ INITIATE SCAN 的行为 \_ 。

***<em>完成和状态</em>***

Scan status 属性 [**KSPROPERTY \_ 调谐器 \_ scan \_ status**](ksproperty-tuner-scan-status.md) 提供有关信号锁定的当前频率和状态的信息。 应用程序从 KSPROPERTY \_ 调谐器 \_ 扫描状态属性查询锁定状态 \_ 。 该应用程序还会查询 [**KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式**](ksproperty-tuner-standard-mode.md) 属性，以获取有关自动信号标准检测的信息。 如果在请求的范围内找不到信号，则 \_ KSPROPERTY \_ 调谐器 \_ scan status 属性将返回[**KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)结构的**LockStatus**成员中的 "**调谐器 \_ LockType \_ None** " 值。 如果优化设备可以自动检测信号中的调谐器标准，并且发现备用标准中有信号，则调谐设备本身可以处理对 [**KSPROPERTY \_ 调谐器 \_ 标准**](ksproperty-tuner-standard.md) 属性的任何请求。 优化设备可能无法在 (PLL) 锁定的情况下继续操作，并且可能会指定标准未知。 或者，调谐设备可能会自动调整到不同的信号标准。 此外，优化设备甚至可以获取该信号标准的完全锁定，并确定备用的标准。 在频率范围内有多个信号标准时，可能会出现这种情况。

***<em>边界条件</em>***

如果驱动程序发现通道的中心频率在应用程序提供的范围之外，则驱动程序必须忽略该信号，并移到下一个信号;驱动程序不能在提供的范围内返回最佳的近似值。 当应用程序尝试编译通道列表时，驱动程序必须转到下一信号，以避免通道的重复计数。

由于同样的原因，应用程序必须将查询范围偏移一半的预期通道带宽 (大约 6/2 = 3MHz 用于模拟和数字电视) ，以确保在硬件遇到硬件无法解码的信号时，不会对通道进行双重计数。 在这种情况下，驱动程序很难避免对某些通道进行双重计数。

***<em>多标准 Spectra</em>***

只要发现新的通道或信号，就必须完成扫描操作。 然后，该驱动程序通过 [**KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态**](ksproperty-tuner-scan-status.md) 属性返回扫描状态。 即使驱动程序确定新找到的通道与以前应用的标准不匹配，只要找到新通道，就必须完成扫描。 应用程序必须处理新的通道信息，并且必须重新提交扫描请求以查找信号标准相同的另一个通道。

## <a name="see-also"></a>另请参阅


[**KSEVENT \_ 调谐器 \_ 启动 \_ 扫描 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksevent_tuner_initiate_scan_s)

[**KSEVENTDATA**](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)

[**KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态**](ksproperty-tuner-scan-status.md)

[**KSPROPERTY \_ 调谐器 \_ 扫描 \_ CAP**](ksproperty-tuner-scan-caps.md)

[**KSPROPERTY \_ 调谐器 \_ 标准版**](ksproperty-tuner-standard.md)

[**KSPROPERTY \_ 调谐器 \_ 标准 \_ 模式**](ksproperty-tuner-standard-mode.md)

