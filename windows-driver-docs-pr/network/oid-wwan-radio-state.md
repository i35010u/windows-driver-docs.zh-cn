---
title: OID_WWAN_RADIO_STATE
description: OID_WWAN_RADIO_STATE 设置或返回有关 MB 设备无线电电源状态的信息。
ms.assetid: e6d09ae8-65c8-4544-9581-8937f61f0747
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_RADIO_STATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9a1255d1e8123c565f9ace28db685113aea8018e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216084"
---
# <a name="oid_wwan_radio_state"></a>OID \_ WWAN \_ 无线电 \_ 状态


OID \_ WWAN \_ 无线电 \_ 状态设置或返回有关 MB 设备无线电电源状态的信息。

微型端口驱动程序必须异步处理集和查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 无线电 \_ 状态**](ndis-status-wwan-radio-state.md) 通知，其中包含表示 MB 设备当前无线电电源状态的 [**ndis \_ WWAN \_ 无线电 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state) 结构，而不考虑完成的集或查询请求。

请求设置 MB 设备的无线电电源状态的调用方为微型端口驱动程序提供了一个具有适当信息的 [**NDIS \_ WWAN \_ 设置 \_ 无线电 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state) 结构。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN 无线电电源状态操作](./mb-radio-power-state-operations.md)。

在处理查询或设置操作时，微型端口驱动程序不应访问提供程序网络或订阅服务器标识模块 (SIM 卡) 。

微型端口驱动程序必须在系统重新启动或设备删除和重新插入时保留软件无线电电源状态。 微型端口驱动程序应存储设备的软件无线信息，并在每次重新启动或设备重新插入时，使用它来设置设备软件无线电电源状态。 根据 [**WWAN \_ 无线电 \_ 状态**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_radio_state)中的表，设备的有效无线电电源状态根据软件和硬件无线电电源状态的组合决定。

如果值为 *WwanRadioOn*，微型端口驱动程序必须打开无线电功能，并将 WWAN 无线电状态结构的 **RadioState SwRadioState** 成员 \_ 设置 \_ 为 *WwanRadioOn*。 如果 HwRadioState 成员*WwanRadioOff*，微型端口驱动程序应缓存此电源状态信息，并确保在**RadioState HwRadioState**更改为*WwanRadioOn*时，以物理方式打开无线电电源状态**RadioState** 。

如果值为 *WwanRadioOff*，微型端口驱动程序必须关闭无线电电源状态，并将 **SwRadioState** 成员设置为 *WwanRadioOff*。

请参阅下表，了解微型端口驱动程序所需的无线电状态编程。

**PIN 模式和 PIN 状态的有效组合**

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>HwRadioState 值</th>
<th>SwRadioState 值</th>
<th>整体无线电电源状态</th>
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

 

对于不提供硬件无线电设备的设备，必须始终将 NDIS WWAN 无线电状态结构的 **RadioState. HwRadioState** 成员 \_ \_ \_ 设置为 *WwanRadioOn*。

从 Windows 10 版本1703开始，OID \_ WWAN \_ 无线电 \_ 状态对于多执行程序支持的调制解调器应如何处理来自 OS 的无线电状态配置具有其他规范。

对于多执行程序支持的调制解调器，为每个执行器配置无线电电源状态有一些优点。 当执行器的无线电关闭后，操作系统会要求调制解调器从网络中取消注册，并且不会尝试从网络中进行任何扫描或位置更新。 该调制解调器应支持它向 OS 播发的每个执行器的无线电状态，以便它可以确定硬件的电源状态。

例如，如果调制解调器有两个执行器，而另一个执行器的无线电在另一个处于打开状态时关闭，则调制解调器可能会让 RF 前端保持开启状态，以便在其无线电打开的执行程序上保持注册，但不需要对关闭的执行程序执行扫描/ping/位置更新或其他移动服务服务。 如果两台无线电装置都处于关闭状态，则调制解调器可以关闭其 RF 前端，并使整体硬件处于较低的电源状态。 实现细节留给每个 IHV。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ WWAN \_ 无线电 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)

[**NDIS \_ WWAN \_ 设置 \_ 无线电 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state)

[**NDIS \_ 状态 \_ WWAN \_ 无线电 \_ 状态**](ndis-status-wwan-radio-state.md)

[WWAN 无线电电源状态操作](./mb-radio-power-state-operations.md)

[**WWAN \_ 无线电 \_ 状态**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_radio_state)

 

