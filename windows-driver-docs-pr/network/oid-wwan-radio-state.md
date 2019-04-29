---
title: OID_WWAN_RADIO_STATE
description: OID_WWAN_RADIO_STATE 设置或返回 MB 设备的无线电电源状态有关的信息。
ms.assetid: e6d09ae8-65c8-4544-9581-8937f61f0747
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_RADIO_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0125e02889c4f9980b1008ec74ef3f698cd9c593
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354527"
---
# <a name="oidwwanradiostate"></a>OID\_WWAN\_RADIO\_STATE


OID\_WWAN\_单选\_状态设置或返回 MB 设备的无线电电源状态有关的信息。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_单选\_状态**](ndis-status-wwan-radio-state.md)状态通知包含[ **NDIS\_WWAN\_单选\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567915)结构，指示当前单选 MB 设备的电源状态而不考虑完成集或查询请求。

调用方请求设置 MB 设备的无线电电源状态提供[ **NDIS\_WWAN\_设置\_单选\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567925)结构微型端口驱动程序的相应信息。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 无线电电源状态操作](https://msdn.microsoft.com/library/windows/hardware/ff559107)。

微型端口驱动程序不能访问提供程序网络或用户识别模块 （SIM 卡），当处理查询或设置操作。

微型端口驱动程序必须跨系统重新启动或设备删除和重新插入时保留软件无线电电源状态。 微型端口驱动程序应存储设备的软件无线电收发器信息并将其用于设置设备软件无线电电源状态立即在每次重新启动或重新插入时的设备。 设备的有效单选电源状态决定基于根据表中的软件和硬件单选电源状态的组合[ **WWAN\_单选\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff571225)。

如果值为*WwanRadioOn*，微型端口驱动程序必须打开单选电源，并将**RadioState.SwRadioState** WWAN 成员\_单选\_状态结构*WwanRadioOn*。 如果**RadioState.HwRadioState**成员已*WwanRadioOff*，微型端口驱动程序应缓存此电源状态信息并确保以物理方式启用单选电源状态时**RadioState.HwRadioState**更改为*WwanRadioOn*。

如果值为*WwanRadioOff*，微型端口驱动程序必须关闭单选电源状态和设置**RadioState.SwRadioState**成员添加到*WwanRadioOff*。

请参阅下表中的编程的微型端口驱动程序的预期的单选状态。

**PIN 模式和锁定状态的有效组合**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>HwRadioState value</th>
<th>SwRadioState value</th>
<th>总体单选电源状态</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WwanRadioOff</p></td>
<td><p>WwanRadioOff</p></td>
<td><p>WwanRadioOff</p></td>
</tr>
<tr class="even">
<td><p>WwanRadioOff</p></td>
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOff</p></td>
</tr>
<tr class="odd">
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOff</p></td>
<td><p>WwanRadioOff</p></td>
</tr>
<tr class="even">
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOn</p></td>
<td><p>WwanRadioOn</p></td>
</tr>
</tbody>
</table>

 

适用于不提供硬件单选电源开关的设备**RadioState.HwRadioState**成员的 NDIS\_WWAN\_单选\_状态结构必须始终设置为*WwanRadioOn*。

从 Windows 10 版本 1703，OID\_WWAN\_单选\_状态具有其他规范，对于多执行器如何支持调制解调器应处理与操作系统单选状态配置。

使用多执行器支持的调制解调器，有 power 好处配置每个执行器单选电源状态。 执行器的单选处于关闭状态，当操作系统需要的调制解调器，若要取消注册从网络并不会尝试从它的任何扫描或位置更新。 调制解调器应为每个执行器，也因此它可以确定硬件电源状态应在其中它会公布到 OS 支持单选状态。

例如，如果调制解调器具有两个执行器和执行器的单选之一时关闭了另一种是，则调制解调器可能保留到提供支持的 RF 前端维护其单选但不需要进行扫描/执行 ping 操作/位置更新该执行器上的注册s 或其他移动电话服务的执行器处于关闭状态。 如果这两个无线电收发器处于关闭状态，调制解调器可以关闭其 RF 前端和整体硬件置于低功率状态。 为每个 IHV 也会保留实现的细节。

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
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_RADIO\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567915)

[**NDIS\_WWAN\_SET\_RADIO\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff567925)

[**NDIS\_STATUS\_WWAN\_RADIO\_STATE**](ndis-status-wwan-radio-state.md)

[WWAN 无线电电源状态操作](https://msdn.microsoft.com/library/windows/hardware/ff559107)

[**WWAN\_RADIO\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff571225)

 

 




