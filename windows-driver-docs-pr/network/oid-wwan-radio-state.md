---
title: OID_WWAN_RADIO_STATE
description: OID_WWAN_RADIO_STATE 设置或返回有关 MB 设备无线电电源状态的信息。
ms.assetid: e6d09ae8-65c8-4544-9581-8937f61f0747
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_RADIO_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7e12e3aaee5a7bba80355036d6b7c59c809f75db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843804"
---
# <a name="oid_wwan_radio_state"></a>OID\_WWAN\_收音机\_状态


OID\_WWAN\_收音机\_状态设置或返回有关 MB 设备无线电电源状态的信息。

微型端口驱动程序必须异步处理集和查询请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[**ndis\_状态\_WWAN\_广播\_状态**](ndis-status-wwan-radio-state.md)通知，其中包含一个[**NDIS\_WWAN\_无线电\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)结构，该结构指示 MB 设备当前无线电电源状态，而不考虑完成的集或查询请求。

请求设置 MB 设备的无线电电源状态的调用方提供[**NDIS\_WWAN\_使用适当的信息将\_无线电\_状态结构设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state)为微型端口驱动程序。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 无线电电源状态操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-radio-power-state-operations)。

在处理查询或设置操作时，微型端口驱动程序不应访问提供程序网络或订阅服务器标识模块（SIM 卡）。

微型端口驱动程序必须在系统重新启动或设备删除和重新插入时保留软件无线电电源状态。 微型端口驱动程序应存储设备的软件无线信息，并在每次重新启动或设备重新插入时，使用它来设置设备软件无线电电源状态。 根据[**WWAN\_无线电\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_radio_state)中的表，设备的有效无线电电源状态根据软件和硬件无线电电源状态的组合决定。

如果值为*WwanRadioOn*，微型端口驱动程序必须启用无线电功能，并将 WWAN\_收音机\_状态结构的**SwRadioState**成员设置为*WwanRadioOn*。 如果 HwRadioState 成员是*WwanRadioOff*，则微型端口驱动程序应缓存此电源状态信息，并确保在**RadioState HwRadioState**更改为 WwanRadioOn 时，以物理方式打开无线电电源状态**RadioState**.

如果值为*WwanRadioOff*，微型端口驱动程序必须关闭无线电电源状态，并将**SwRadioState**成员设置为*WwanRadioOff*。

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

 

对于未提供硬件无线电电源开关的设备，\_WWAN\_收音机\_状态结构的 NDIS 的**HwRadioState**成员必须始终设置为*WwanRadioOn*。

从 Windows 10 1703 版开始，OID\_WWAN\_无线电\_状态对于多执行程序支持的调制解调器应如何处理来自 OS 的无线电状态配置有其他规范。

对于多执行程序支持的调制解调器，为每个执行器配置无线电电源状态有一些优点。 当执行器的无线电关闭后，操作系统会要求调制解调器从网络中取消注册，并且不会尝试从网络中进行任何扫描或位置更新。 该调制解调器应支持它向 OS 播发的每个执行器的无线电状态，以便它可以确定硬件的电源状态。

例如，如果调制解调器有两个执行器，而另一个执行器的无线电在另一个处于打开状态时关闭，则调制解调器可能会让 RF 前端保持开启状态，以便在其无线电设备开启的执行程序上保持注册，但不需要进行扫描/ping/位置更新s 或关闭的执行器的其他移动服务服务。 如果两台无线电装置都处于关闭状态，则调制解调器可以关闭其 RF 前端，并使整体硬件处于较低的电源状态。 实现细节留给每个 IHV。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_收音机\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_radio_state)

[**NDIS\_WWAN\_集\_无线电\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_radio_state)

[ **\_WWAN\_无线电\_状态的 NDIS\_状态**](ndis-status-wwan-radio-state.md)

[WWAN 无线电电源状态操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-radio-power-state-operations)

[**WWAN\_无线电\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_radio_state)

 

 




