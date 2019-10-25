---
title: OID_WWAN_PIN
description: OID_WWAN_PIN 设置或返回与个人标识号（Pin）相关的信息。
ms.assetid: 5c93ffe0-8067-4022-ba8e-e528e44692e6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PIN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d2dfc86d22a39a70a7dff7431cda9307c421f975
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843814"
---
# <a name="oid_wwan_pin"></a>OID\_WWAN\_PIN


OID\_WWAN\_PIN 集或返回与个人标识号（Pin）相关的信息。

微型端口驱动程序必须异步处理集和查询请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[**ndis\_状态\_WWAN\_PIN 发送\_信息**](ndis-status-wwan-pin-info.md)状态通知完成了设置或查询请求。

微型端口驱动程序应将[**ndis\_状态发送\_WWAN\_PIN\_信息**](ndis-status-wwan-pin-info.md)状态通知，其中包含[**NDIS\_WWAN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)\_信息，主要用于指示在完成查询请求时是否需要 PIN 来解锁 MB 设备或订户标识模块（SIM 卡）。

请求设置与 Pin 相关的信息的调用方提供[**NDIS\_WWAN\_将\_pin 结构设置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin)为微型端口驱动程序以将 pin 发送到 MB 设备、启用或禁用 pin 设置，或者更改 SIM 上的 pin。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN Pin 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)。

Windows 7 微型端口驱动程序应使用 OID\_WWAN\_PIN。 Windows 8 微型端口驱动程序应使用[OID\_WWAN\_PIN\_EX](oid-wwan-pin-ex.md)

当处理查询操作时，微型端口驱动程序可以访问订阅服务器标识模块（SIM 卡），但不应访问提供程序网络。

在微型端口驱动程序初始化过程中，如果启用了 PIN1，则 MB 服务不会继续进行注册。

小型端口驱动程序提供由最终用户输入的 PIN 值，位于 NDIS\_WWAN\_在处理设置请求时设置\_PIN**结构。** 仅当 PIN 值与 SIM 卡中存储的值匹配时，才应由微型端口驱动程序处理请求。 否则，微型端口驱动程序应失败，状态代码为 WWAN\_状态\_失败的设置请求。

基于 CDMA 的设备必须将电源设备锁定报告为 PIN1。

对于所有受支持的 PIN 类型，微型端口驱动程序必须支持*WwanPinOperationEnter*操作。 此外，如果支持 PIN1，微型端口驱动程序必须支持*WwanPinOperationEnable*、 *WwanPinOperationDisable*和*WwanPinOperationChange*操作。

如果在 PIN 类型锁定时尝试 pin 类型的 PIN 禁用操作，微型端口驱动程序可以使用 WWAN\_状态使请求失败\_PIN\_必需的，或者它们可以成功完成请求。 如果微型端口驱动程序已成功完成请求，则禁用操作还应解除锁定。

如果已启用报表多个 pin，并且一次只能报告一个 PIN，则微端口驱动程序应首先报告 PIN1。 例如，如果启用了 SubsidyLock 和 SIM PIN1 的报告，则仅在成功验证 PIN1 后，才应报告 SubsidyLock PIN （在后续查询请求中）。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_固定\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_pin_info)

[**NDIS\_WWAN\_集\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_pin)

[ **\_WWAN\_PIN\_信息的 NDIS\_状态**](ndis-status-wwan-pin-info.md)

[WWAN Pin 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-pin-operations)

 

 




