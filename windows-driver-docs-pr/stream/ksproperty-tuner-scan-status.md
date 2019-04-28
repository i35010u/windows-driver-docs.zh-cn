---
title: KSPROPERTY\_调谐器\_扫描\_状态
description: KSPROPERTY\_调谐器\_扫描\_状态属性描述扫描操作的状态。 可以根据需要实现此属性。
ms.assetid: ce7dd30b-84fc-46e2-847c-33c07e60e0f7
keywords:
- KSPROPERTY_TUNER_SCAN_STATUS 流式处理媒体设备
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
ms.openlocfilehash: b2bd64fcae87c8b88a898e70cc4082719bc0c80b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342197"
---
# <a name="kspropertytunerscanstatus"></a>KSPROPERTY\_调谐器\_扫描\_状态


KSPROPERTY\_调谐器\_扫描\_状态属性描述扫描操作的状态。 可以根据需要实现此属性。

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
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565898" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_STATUS_S&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565898)"><strong>KSPROPERTY_TUNER_SCAN_STATUS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_STATUS_S</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是 KSPROPERTY\_调谐器\_扫描\_状态\_S 结构，它指定扫描操作的状态。

<a name="remarks"></a>备注
-------

*KsTvTune.ax*模块可以调用驱动程序的 KSPROPERTY\_调谐器\_扫描\_STATUS 属性在任何时间。 但是， *KsTvTune.ax*通常会调用 KSPROPERTY\_调谐器\_扫描\_状态后，它调用[ **KSEVENT\_调谐器\_启动\_扫描**](ksevent-tuner-initiate-scan.md)事件设置扫描操作，并设置当扫描完成时的通知。 *KsTvTune.ax*然后等待扫描完成通知发生。 坏的情况下，作为*KsTvTune.ax*中指定的时间量内等待**SettlingTime**的成员[**调谐器\_模拟\_CAPS\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff568547)结构。 该驱动程序应返回填充的调谐器\_模拟\_CAPS\_S 通过调用其[ **KSPROPERTY\_调谐器\_NETWORKTYPE\_扫描\_CAPS** ](ksproperty-tuner-networktype-scan-caps.md)属性与模拟\_电视\_网络\_中设置类型值**NetworkType**的成员[ **KSPROPERTY\_调谐器\_NETWORKTYPE\_扫描\_CAPS\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565885)结构。 但是，该调谐器通常应确定比中指定的时间量更快的信号的状态**SettlingTime** ，然后应通知*KsTvTune.ax*扫描完成通过发出事件信号。

仅当优化设备支持硬件辅助扫描，驱动程序返回的扫描状态。 该驱动程序通过设置来指示此类支持**fSupportsHardwareAssistedScanning**的成员[ **KSPROPERTY\_调谐器\_扫描\_CAPS\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565892)结构**TRUE**的调用中其[ **KSPROPERTY\_调谐器\_扫描\_CAPS**](ksproperty-tuner-scan-caps.md)属性。 驱动程序应发出信号事件并返回一个中的以下锁定类型**LockStatus**的成员[ **KSPROPERTY\_调谐器\_扫描\_状态\_S** ](https://msdn.microsoft.com/library/windows/hardware/ff565898)结构：

-   **调谐器\_LockType\_None**如果优化设备根本无法找到任何信号。

-   **调谐器\_LockType\_已锁定**如果优化设备锁定到确切的频率。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本的操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSEVENT\_调谐器\_启动\_扫描**](ksevent-tuner-initiate-scan.md)

[**KSPROPERTY\_TUNER\_NETWORKTYPE\_SCAN\_CAPS**](ksproperty-tuner-networktype-scan-caps.md)

[**KSPROPERTY\_TUNER\_NETWORKTYPE\_SCAN\_CAPS\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565885)

[**KSPROPERTY\_调谐器\_扫描\_CAP**](ksproperty-tuner-scan-caps.md)

[**KSPROPERTY\_调谐器\_扫描\_CAPS\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565892)

[**KSPROPERTY\_调谐器\_扫描\_状态\_S**](https://msdn.microsoft.com/library/windows/hardware/ff565898)

[**调谐器\_模拟\_CAPS\_S**](https://msdn.microsoft.com/library/windows/hardware/ff568547)

 

 






