---
title: KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态
description: KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态属性描述扫描操作的状态。 此属性可以选择实现。
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
ms.openlocfilehash: c432b76ee652d60cb3ae07c5dc3b38d5e2df5fc0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823687"
---
# <a name="ksproperty_tuner_scan_status"></a>KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态


KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态属性描述扫描操作的状态。 此属性可以选择实现。

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
<th>获取</th>
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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_SCAN_STATUS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)"><strong>KSPROPERTY_TUNER_SCAN_STATUS_S</strong></a></p></td>
<td><p>KSPROPERTY_TUNER_SCAN_STATUS_S</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态 \_ S 结构，它指定扫描操作的状态。

<a name="remarks"></a>备注
-------

*KsTvTune.ax* 模块可随时调用驱动程序的 KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态属性。 但是， *KsTvTune.ax* 通常 \_ \_ \_ 会在调用 [**KSEVENT \_ 调谐器 \_ INITIATE \_ scan**](ksevent-tuner-initiate-scan.md) 事件之后调用 KSPROPERTY 调谐器扫描状态，以设置扫描操作并设置扫描完成时的通知。 *KsTvTune.ax* 然后等待扫描完成通知发生。 最糟糕的情况是， *KsTvTune.ax* 会等待 [**调谐器 \_ 模拟 \_ cap \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tuner_analog_caps_s)结构的 **SettlingTime** 成员中指定的时间量。 驱动程序应已 \_ \_ 从对 \_ 其 [**KSPROPERTY \_ 调谐器 \_ NETWORKTYPE \_ scan \_ cap**](ksproperty-tuner-networktype-scan-caps.md)属性的调用返回填充的调谐器模拟 cap，并在 \_ \_ \_ [**KSPROPERTY \_ 调谐器 \_ NETWORKTYPE \_ 扫描 \_ 端 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_networktype_scan_caps_s)结构的 **NETWORKTYPE** 成员中设置了模拟 TV 网络类型值。 但是，通常情况下，调谐器会确定信号的状态，这比在 **SettlingTime** 中指定的时间更快，并应通过发出事件信号通知 *KsTvTune.ax* 已完成扫描。

仅当优化设备支持硬件辅助扫描时，驱动程序才会返回扫描状态。 驱动程序通过在对其 [**KSPROPERTY \_ 调谐器 \_ 扫描 \_ cap**](ksproperty-tuner-scan-caps.md)属性的调用中将 [**KSPROPERTY \_ 调谐器 \_ Scan \_ \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)结构的 **fSupportsHardwareAssistedScanning** 成员设置为 **TRUE** 来指示此类支持。 驱动程序应向事件发出信号，并在 [**KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)结构的 **LockStatus** 成员中返回以下锁类型之一：

-   **调谐器 \_如果 \_** 优化设备根本找不到任何信号，则 LockType "无"。

-   **调谐器 \_如果 \_** 优化设备锁定到确切频率，则 LockType 锁定。

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
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSEVENT \_ 调谐器 \_ 启动 \_ 扫描**](ksevent-tuner-initiate-scan.md)

[**KSPROPERTY \_ 调谐器 \_ NETWORKTYPE \_ 扫描 \_ CAP**](ksproperty-tuner-networktype-scan-caps.md)

[**KSPROPERTY \_ 调谐器 \_ NETWORKTYPE \_ 扫描 \_ CAP \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_networktype_scan_caps_s)

[**KSPROPERTY \_ 调谐器 \_ 扫描 \_ CAP**](ksproperty-tuner-scan-caps.md)

[**KSPROPERTY \_ 调谐器 \_ 扫描 \_ CAP \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_caps_s)

[**KSPROPERTY \_ 调谐器 \_ 扫描 \_ 状态 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_scan_status_s)

[**调谐器 \_ 模拟 \_ CAP \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tuner_analog_caps_s)

