---
title: OID_WWAN_PROVISIONED_CONTEXTS
description: OID_WWAN_PROVISIONED_CONTEXTS 读取或更新存储在 MB 设备或订阅服务器标识模块 (SIM) 上的预配上下文条目。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PROVISIONED_CONTEXTS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3a72649a6c042ec2b8697993b4d5ad04653a3cb4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812949"
---
# <a name="oid_wwan_provisioned_contexts"></a>OID \_ WWAN \_ 预配 \_ 上下文


OID \_ WWAN \_ 预配 \_ 上下文读取或更新存储在 MB 设备或订阅服务器标识模块 (SIM) 上的预配上下文条目。

微型端口驱动程序必须异步处理 set 和 query 请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ wwan \_ 预 \_ 配**](ndis-status-wwan-provisioned-contexts.md) 上下文状态通知，其中包含 [**ndis \_ WWAN \_ 预 \_**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts) 配的上下文状态通知，其中包含存储在 MB 设备或订阅服务器标识模块 (SIM) 的预配上下文条目的相关信息，而不考虑完成集或查询请求。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN 数据包上下文管理](./mb-packet-context-management.md)。

\_ \_ \_ 如果端口支持的 MB 设备不支持检索预配的上下文，则微型端口驱动程序应返回不受支持的 NDIS 状态。

基于 GSM 的设备可以选择支持查询和设置操作。 基于 CDMA 的设备可以选择支持报告简单 IP (WWAN \_ CTRL \_ cap \_ CDMA \_ 简单 \_ ip) 的查询操作。

存储在 MB 设备上的预配上下文条目或 SIM 在设备本地。 小型端口驱动程序不应连接到网络来读取这些字段。

设置请求的输入结构为 NDIS \_ WWAN \_ 设置 \_ 预配 \_ 上下文，此对象的状态指示为 ndis \_ 状态 \_ WWAN \_ 预配 \_ 的上下文。

预配的上下文与缓存 APNs 列表的3GPP 中的 GPRS 上下文定义不同。 预配的上下文是 (AccessString、UserName 和 Password) 的连接参数，这些参数可以由设备预配的操作员或 OTA 预配，并且可以存储在设备内存或 SIM 中。 MB 服务将使用由预配的上下文返回的连接参数进行 PDP 激活。

使用此对象的查询和设置形式。

此请求的处理不需要网络访问，但需要在 MB 设备上访问 SIM 或辅助内存。

微型端口驱动程序将 NDIS \_ 状态 \_ WWAN \_ 预配 \_ 上下文通知发送到操作系统。 **ContextListHeader** 成员应设置为 *WwanStructContext*。 当发送通知以响应某个设置请求时，微型端口驱动程序应将 **elementcount 多于** 成员设置为0。

在执行任何单个上下文激活或停用之前，MB 服务应从设备检索预配的上下文列表。 预配上下文的列表必须仅限制为主提供商网络，即使设备可能能够存储多个网络提供程序上下文。 上下文列表必须始终是特定于家乡提供商网络的，即使是漫游也是如此。

设置 OID \_ wwan \_ 预配 \_ 上下文操作应将上下文与在 WWAN 集上下文的 **ProviderId** 成员中的 set 请求中指定的网络提供程序相关联 \_ \_ 。 通过设置 OID \_ WWAN \_ 预配的上下文请求存储的预配上下文 \_ 必须跨系统重新启动和设备电源回收保持。

所有空上下文都需要在查询上报告，并与适用于 home 提供商网络的预配上下文一起报告。

CDMA 配置为 SimpleIP 的设备，在 \_ WwanControlCaps 中的 "WWAN" CTRL + a \_ \_ CDMA SIMPLE IP 中进行报告， \_ \_ 可以选择性地返回至少一个预配的上下文，其中填充了来自 MB 服务的查询请求的正确 **AccessString**、 **用户名** 和 **密码** 成员。

预配的上下文列表应在设备中预配，通过设置 OID \_ WWAN \_ 预配 \_ 上下文操作进行更新，或通过使用 SMS 或 OTA 通过设备/操作员进行更新。 不能基于 OID \_ WWAN \_ CONNECT Operation MB 服务中提供的上下文信息进行动态更新。

若要详细了解如何从 MB 设备访问列表中每个预配上下文的 AccessString、UserName 和 Password，请参阅 [**WWAN \_ 上下文**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_context)。

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


[WWAN 数据包上下文管理](./mb-packet-context-management.md)

 

