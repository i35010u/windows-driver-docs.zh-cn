---
title: OID_WWAN_PIN
description: OID_WWAN_PIN 设置或返回与 (Pin) 的个人识别码相关的信息。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PIN 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3c0a5191abd9be8b40e98e8a78faa2e4041f017b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809929"
---
# <a name="oid_wwan_pin"></a>OID \_ WWAN \_ PIN


OID \_ WWAN \_ PIN 设置或返回与)  (Pin 的个人识别码相关的信息。

微型端口驱动程序必须异步处理集和查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后在完成了 set 或 query 请求后发送 [**ndis \_ 状态 \_ WWAN \_ PIN \_ 信息**](ndis-status-wwan-pin-info.md) 状态通知。

微型端口驱动程序应发送 [**ndis \_ 状态 \_ WWAN \_ pin \_ 信息**](ndis-status-wwan-pin-info.md) 状态通知，其中包含 [**NDIS \_ WWAN \_ pin \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info) 结构来返回 pin 类型和 pin 输入状态信息，主要用于指示在完成查询请求时，是否需要 PIN 来解锁 MB 设备或订户标识模块 (SIM 卡) 。

请求设置与 Pin 相关的信息的调用方为微型端口驱动程序提供 [**NDIS \_ WWAN \_ 集 \_ pin**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin) 结构，以将 pin 发送到 MB 设备，启用或禁用 PIN 设置，或者更改 SIM 上的 pin。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN Pin 操作](./mb-pin-operations.md) 。

Windows 7 微型端口驱动程序应使用 OID \_ WWAN \_ PIN。 Windows 8 微型端口驱动程序应使用[OID \_ WWAN \_ PIN （ \_ 例如](oid-wwan-pin-ex.md)

当处理查询操作时，微型端口驱动程序可以 (SIM 卡) 访问订阅服务器标识模块，但不应访问提供程序网络。

在微型端口驱动程序初始化过程中，如果启用了 PIN1，则 MB 服务不会继续进行注册。

小型端口驱动程序提供一个 PIN 值，该值由最终用户在 **PinAction.Pin** \_ \_ \_ 处理集请求时在 NDIS WWAN 集 PIN 结构的 PinAction 成员中输入。 仅当 PIN 值与 SIM 卡中存储的值匹配时，才应由微型端口驱动程序处理请求。 否则，微型端口驱动程序应使设置请求失败，状态代码为 WWAN \_ 状态 \_ 失败。

基于 CDMA 的设备必须将电源设备锁定报告为 PIN1。

对于所有受支持的 PIN 类型，微型端口驱动程序必须支持 *WwanPinOperationEnter* 操作。 此外，如果支持 PIN1，微型端口驱动程序必须支持 *WwanPinOperationEnable*、 *WwanPinOperationDisable* 和 *WwanPinOperationChange* 操作。

如果在 PIN 类型锁定时尝试 pin 类型的 PIN 禁用操作，微型端口驱动程序可以使用所需的 WWAN 状态 PIN 来使请求失败， \_ \_ \_ 也可以成功完成请求。 如果微型端口驱动程序已成功完成请求，则禁用操作还应解除锁定。

如果已启用报表多个 pin，并且一次只能报告一个 PIN，则微端口驱动程序应首先报告 PIN1。 例如，如果启用了 "报告 SubsidyLock" 和 "SIM PIN1"，则应在后续查询请求中 (报告 SubsidyLock PIN，仅在成功验证 PIN1 后) 。

除 PIN1 外，MB API 还支持其他 Pin。 但是，需要安装第三方连接管理器/GUI，因为 Windows 连接管理器/GUI 仅支持 PIN1。

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

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ PIN \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)

[**NDIS \_ WWAN \_ 设置 \_ PIN**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin)

[**NDIS \_ 状态 \_ WWAN \_ PIN \_ 信息**](ndis-status-wwan-pin-info.md)

[WWAN Pin 操作](./mb-pin-operations.md)

 

