---
title: OID_WWAN_SMS_CONFIGURATION
description: OID_WWAN_SMS_CONFIGURATION 设置或返回一个 MB 设备的 SMS 文本消息配置。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_CONFIGURATION 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cba18f4c0c428906998563c06a440fafcef5d51f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812909"
---
# <a name="oid_wwan_sms_configuration"></a>OID \_ WWAN \_ SMS \_ 配置


OID \_ WWAN \_ sms \_ 配置设置或返回一个 MB 设备的 sms 文本消息配置。

微型端口驱动程序必须异步处理集和查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，并在以后发送 [**ndis \_ 状态 \_ WWAN \_ SMS \_ 配置**](ndis-status-wwan-sms-configuration.md) 状态通知，而不考虑完成的集或查询请求。

查询请求返回存储在设备或订阅服务器标识模块 (SIM) 卡的 MB 设备的当前 SMS 文本消息配置。

设置请求使用 [**NDIS \_ WWAN \_ 设置 \_ sms \_ 配置**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration) 结构来更改 MB 设备的 SMS 文本消息配置。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN SMS 操作](./mb-sms-operations.md)。

当处理此 OID 时，微型端口驱动程序可以访问 SIM 卡，但不应访问提供程序网络。

基于 GSM 的设备的微型端口驱动程序应支持查询和设置操作。 基于 CDMA 的设备的微型端口驱动程序应仅支持查询操作。 基于 CDMA 的设备的微型端口驱动程序应在查询请求的 WWAN SMS 配置结构的 **ulMaxMessageIndex** 成员中返回有效的值 \_ \_ ，并且可以忽略其他成员。

\_ \_ \_ \_ 当 MB 设备的 sms 子系统准备好执行 SMS 操作时，微型端口驱动程序必须发送未经请求的 NDIS 状态 WWAN SMS 配置指示。 此后，当响应 OID \_ WWAN \_ sms \_ 配置查询请求时，微型端口驱动程序必须为 WWAN \_ sms 配置结构的所有成员返回有效值 \_ 。

\_ \_ \_ 如果已初始化设备，但 SMS 子系统尚未初始化，则微型端口驱动程序应返回 NDIS 状态 "未初始化"。

如果微型端口驱动程序 \_ 不 \_ \_ 支持配置 SMS 文本消息，则它应返回不受支持的 NDIS 状态。

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


[**NDIS \_ WWAN \_ 设置 \_ SMS \_ 配置**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration)

[**NDIS \_ 状态 \_ WWAN \_ SMS \_ 配置**](ndis-status-wwan-sms-configuration.md)

[WWAN SMS 操作](./mb-sms-operations.md)

 

