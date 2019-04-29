---
title: OID_WWAN_PROVISIONED_CONTEXTS
description: OID_WWAN_PROVISIONED_CONTEXTS 读取或更新存储在 MB 设备或订阅服务器上标识模块 (SIM) 上的预配的上下文项。
ms.assetid: 7634fc32-9059-4f89-a591-7aa663b0c188
ms.date: 08/08/2017
keywords: -OID_WWAN_PROVISIONED_CONTEXTS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 78ea8f12f45601342fe47b3e6e0abd8baabd0adb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354535"
---
# <a name="oidwwanprovisionedcontexts"></a>OID\_WWAN\_已设置\_上下文


OID\_WWAN\_已设置\_上下文读取或更新存储在 MB 设备或订阅服务器上标识模块 (SIM) 上的预配的上下文项。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_已预配\_上下文**](ndis-status-wwan-provisioned-contexts.md)状态通知包含[ **NDIS\_WWAN\_已预配\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff567914)结构，以提供有关预配的上下文项存储在 MB 设备或而不考虑完成集或查询的请求订阅服务器上标识模块 (SIM) 上的信息。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN 数据包上下文管理](https://msdn.microsoft.com/library/windows/hardware/ff559086)。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们支持的 MB 设备不支持的预配的上下文检索支持。

基于 GSM 的设备可以根据需要支持查询和设置操作。 基于 CDMA 的设备可以选择性地支持查询操作报告简单 IP (WWAN\_CTRL\_CAPS\_CDMA\_简单\_IP)。

在设备本地存储在 MB 设备或 sim 卡上的预配的上下文项。 微型端口驱动程序不应连接到网络，以便在这些字段中读取。

设置请求的输入的结构所 NDIS\_WWAN\_设置\_已预配\_的此对象的上下文和状态指示是 NDIS\_状态\_WWAN\_已预配\_上下文。

预配的上下文不是为与 3GPP 缓存 APNs 的列表中的 GPRS 上下文定义相同的。 预配的上下文是连接参数 （AccessString、 用户名和密码） 可以预配了运算符或 OTA 设备预配，可以存储在设备内存或 SIM。 PDP 激活，MB 服务将使用返回的已设置上下文的连接参数。

两种查询和使用此对象的集窗体。

此请求的处理不需要网络访问权限，但需要访问 SIM 或 MB 设备上的辅助内存。

微型端口驱动程序将发送 NDIS\_状态\_WWAN\_已设置\_上下文通知到操作系统。 **ContextListHeader.ElementType**成员应设置为*WwanStructContext*。 微型端口驱动程序应设置**ContextListHeader.ElementCount**为 0 时通知发送到集请求的响应中的成员。

在执行任何单个上下文激活或停用之前，MB 服务应从设备检索预配的上下文的列表。 预配的上下文的列表必须仅限于家庭的提供程序网络，即使该设备可能有存储多个网络提供程序上下文的功能。 上下文列表必须始终为特定甚至发生漫游时的家庭的提供程序网络。

设置 OID\_WWAN\_已预配\_上下文操作应将上下文中的集请求中指定的网络提供程序与关联**ProviderId** WWAN成员\_设置\_上下文结构。 通过存储预配的上下文设置 OID\_WWAN\_已设置\_上下文的请求必须在系统中保持原样的重启和设备电源回收。

所有空上下文需要报告上一个查询以及适用于家庭的提供程序网络的预配的上下文。

为 SimpleIP，WWAN 中的报表配置的 CDMA 设备\_CTRL\_CAPS\_CDMA\_简单\_中 WwanControlCaps IP 可以选择性地返回至少一个预配的上下文使用填充正确**AccessString**，**用户名**，并**密码**来自 MB 服务的查询请求的成员。

预配的上下文列表应进行预配在设备中，更新由组 OID\_WWAN\_已设置\_上下文操作或更新的设备/操作员使用短信或 OTA。 它必须更新根据 OID 中提供的上下文信息动态\_WWAN\_MB 服务的连接操作。

有关如何访问 AccessString、 用户名和密码，从列表中每个预配的上下文的 MB 设备的详细信息，请参阅[ **WWAN\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff571201)。

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


[WWAN 数据包上下文管理](https://msdn.microsoft.com/library/windows/hardware/ff559086)

 

 




