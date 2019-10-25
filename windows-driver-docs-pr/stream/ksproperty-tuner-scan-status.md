---
title: KSPROPERTY\_调谐器\_扫描\_状态
description: KSPROPERTY\_调谐器\_SCAN\_STATUS 属性介绍了扫描操作的状态。 此属性可以选择实现。
ms.assetid: ce7dd30b-84fc-46e2-847c-33c07e60e0f7
keywords:
- KSPROPERTY_TUNER_SCAN_STATUS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_SCAN_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c06b6766e4ea3833714e08661a4ab19e67c74e1f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837904"
---
# <a name="ksproperty_tuner_scan_status"></a>KSPROPERTY\_调谐器\_扫描\_状态


KSPROPERTY\_调谐器\_SCAN\_STATUS 属性介绍了扫描操作的状态。 此属性可以选择实现。

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
<td><p>“是”</p></td>
<td><p>无</p></td>
<td><p>大头针</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_STATUS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)"><strong>KSPROPERTY_TUNER_SCAN_STATUS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_STATUS_S</p></td>
</tr>
</tbody>
</table>

 

属性值（操作数据）是一种 KSPROPERTY\_调谐器\_扫描\_状态\_S 结构，用于指定扫描操作的状态。

<a name="remarks"></a>备注
-------

*KsTvTune.ax*模块可随时调用驱动程序的 KSPROPERTY\_调谐器\_扫描\_状态属性。 但是， *KsTvTune.ax*通常会调用 KSPROPERTY\_调谐器\_在其调用 KSEVENT\_调谐器后扫描\_状态[ **\_启动\_scan**](ksevent-tuner-initiate-scan.md)事件，以设置扫描操作并设置通知。扫描完成。 *KsTvTune.ax*然后等待扫描完成通知发生。 最糟糕的情况是， *KsTvTune.ax*会等待调谐器的**SettlingTime**成员中指定的时间量[ **\_模拟\_cap\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tuner_analog_caps_s)结构。 驱动程序应使用模拟\_\_\_网络，从\_模拟\_CAP\_S 返回填充的调谐器，并将其从[**KSPROPERTY\_调谐器调用\_NETWORKTYPE\_** ](ksproperty-tuner-networktype-scan-caps.md)KSPROPERTY\_调谐器\_NETWORKTYPE 的**NetworkType**成员中设置的 __t_11_ 类型值[ **\_SCAN\_cap\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_networktype_scan_caps_s)结构。 但是，通常情况下，调谐器会确定信号的状态，这比在**SettlingTime**中指定的时间更快，并应通过发出事件信号通知*KsTvTune.ax*已完成扫描。

仅当优化设备支持硬件辅助扫描时，驱动程序才会返回扫描状态。 驱动程序通过将 KSPROPERTY\_调谐器的**fSupportsHardwareAssistedScanning**成员设置为在对其 KSPROPERTY 的调用中[ **\_扫描\_Cap\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)为**TRUE**来指示此类支持[ **\_调谐器\_扫描\_CAP**](ksproperty-tuner-scan-caps.md)属性。 驱动程序应向事件发出信号，并在 KSPROPERTY\_调谐器的**LockStatus**成员中返回以下锁类型之一[ **\_扫描\_状态\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)结构：

-   如果优化设备根本找不到任何信号，则**调谐器\_LockType\_"无**"。

-   如果优化设备锁定到确切的频率，**调谐器\_LockType\_锁定**。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia （包括 Ksmedia）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**KSEVENT\_调谐器\_启动\_扫描**](ksevent-tuner-initiate-scan.md)

[**KSPROPERTY\_调谐器\_NETWORKTYPE\_扫描\_CAP**](ksproperty-tuner-networktype-scan-caps.md)

[**KSPROPERTY\_调谐器\_NETWORKTYPE\_扫描\_CAP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_networktype_scan_caps_s)

[**KSPROPERTY\_调谐器\_扫描\_CAP**](ksproperty-tuner-scan-caps.md)

[**KSPROPERTY\_调谐器\_扫描\_CAP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)

[**KSPROPERTY\_调谐器\_扫描\_状态\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)

[**调谐器\_模拟\_CAP\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tuner_analog_caps_s)

 

 






