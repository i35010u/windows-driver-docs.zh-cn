---
title: OID_WWAN_PIN
description: OID_WWAN_PIN 设置或返回与个人标识号 (Pin) 相关的信息。
ms.assetid: 5c93ffe0-8067-4022-ba8e-e528e44692e6
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PIN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 42e58929faa293234ef314b713186a3b3eea820a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354541"
---
# <a name="oidwwanpin"></a>OID\_WWAN\_PIN


OID\_WWAN\_PIN 设置或返回与个人标识号 (Pin) 相关的信息。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_PIN\_信息**](ndis-status-wwan-pin-info.md)状态通知时他们已完成的集或查询请求。

微型端口驱动程序应发送[ **NDIS\_状态\_WWAN\_PIN\_信息**](ndis-status-wwan-pin-info.md)状态通知包含[ **NDIS\_WWAN\_PIN\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567911)结构返回固定类型和 PIN 输入状态的信息，主要用于指示是否需要 PIN 来解锁的 MB 设备或订阅服务器识别模块 （SIM 卡） 完成查询请求时。

调用方请求设置 Pin 与相关的信息提供[ **NDIS\_WWAN\_设置\_PIN** ](https://msdn.microsoft.com/library/windows/hardware/ff567922)微型端口驱动程序将发送到 MB 设备的 PIN 的结构启用或禁用 PIN 设置或更改在 sim 卡 PIN。

<a name="remarks"></a>备注
-------

请参阅[WWAN Pin 操作](https://msdn.microsoft.com/library/windows/hardware/ff559093)有关使用此 OID 的详细信息。

Windows 7 微型端口驱动程序应使用 OID\_WWAN\_PIN。 Windows 8 微型端口驱动程序应使用[OID\_WWAN\_PIN\_EX](oid-wwan-pin-ex.md)。

微型端口驱动程序可以访问用户识别模块 （SIM 卡） 当处理查询操作，但不是应访问提供程序网络。

在微型端口驱动程序初始化过程中，MB 服务将不会继续到注册直到 PIN1 成功解锁，如果已启用。

微型端口驱动程序提供的 PIN 值，由最终用户进入**PinAction.Pin**成员的 NDIS\_WWAN\_设置\_PIN 结构处理时设置的请求。 仅当的 PIN 值与存储在 SIM 卡中的值匹配时，才应处理该请求由微型端口驱动程序。 否则，微型端口驱动程序应失败，状态代码为 WWAN 集请求\_状态\_失败。

基于 CDMA 的设备必须作为 PIN1 报告设备上的锁。

所有受支持类型 PIN，微型端口驱动程序必须支持*WwanPinOperationEnter*操作。 此外，如果支持 PIN1，微型端口驱动程序必须支持*WwanPinOperationEnable*， *WwanPinOperationDisable*，并*WwanPinOperationChange*操作。

如果 PIN 禁用操作的 PIN 类型会尝试锁定该 PIN 类型时，请微型端口驱动程序或者失败将请求与 WWAN\_状态\_PIN\_必需或它们可以成功完成请求。 如果微型端口驱动程序成功完成请求，禁用操作还应解除锁定 PIN。

如果报告已启用多个插针，并且只有一个 PIN 可以报告一次，然后应微型端口驱动程序第一次报告 PIN1。 例如，如果启用了 SubsidyLock 和 SIM PIN1 的报告，然后 SubsidyLock PIN 中应该报告 （后续查询请求） 才 PIN1 已成功验证。

MB API 支持除了 PIN1 其他 Pin。 但是，第三方连接管理器/GUI 将需要安装，因为 Windows 连接管理器/GUI 支持仅 PIN1。

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


[**NDIS\_WWAN\_PIN\_INFO**](https://msdn.microsoft.com/library/windows/hardware/ff567911)

[**NDIS\_WWAN\_SET\_PIN**](https://msdn.microsoft.com/library/windows/hardware/ff567922)

[**NDIS\_状态\_WWAN\_PIN\_信息**](ndis-status-wwan-pin-info.md)

[WWAN 固定操作](https://msdn.microsoft.com/library/windows/hardware/ff559093)

 

 




