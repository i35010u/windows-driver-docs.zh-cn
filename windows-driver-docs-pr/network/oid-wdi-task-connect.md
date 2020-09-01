---
title: OID_WDI_TASK_CONNECT
description: OID_WDI_TASK_CONNECT IHV 组件连接到访问点或 Wi-fi Direct 中转的请求。
ms.assetid: 63ba3979-6b30-49bf-91a9-fa01f0ef4922
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_CONNECT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: fc8a2b2ed275e552b57748efea4dae5a8bea3db8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213219"
---
# <a name="oid_wdi_task_connect"></a>OID \_ WDI \_ 任务 \_ 连接


OID \_ WDI \_ 任务 \_ CONNECT： IHV 组件连接到访问点或 wi-fi Direct 中转的请求。

| 对象 | 支持中止                                     | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 中止必须后接 dot11 重置。 | 4                                     | 10                              |

 

作为连接的一部分，IHV 组件必须与 BSS 同步，并向其进行身份验证，并将其与 BSS 关联。 主机提供了 IHV 组件可以尝试连接到的 BSS 条目。 在 IHV 组件成功连接到这些条目之一后，它应完成连接过程。 如果无法连接到任何 BSS 条目，则应完成连接过程，并出现故障。

IHV 组件不需要执行扫描即可查找候选 BSS 条目。 它可以使用主机提供的用于连接的列表。 它可以多次尝试连接到每个连接。 主机按 RSSI 对网络进行排序，但 IHV 组件可使用其自己的连接顺序。 如果适配器未指定 "连接 BSS 选择替代"，则它必须只使用主机提供的用于连接的条目。 主机可以在未完成的连接上发出中止。 接收到中止后，端口必须结束连接尝试并将完成情况报告给主机。

如果适配器指定 "连接 BSS 选择替代"，则它可以自行执行扫描以查找候选 BSS 条目。 只要满足主机配置的参数，它就可以连接到它发现的任何 BSS 条目。 它应该优化此选择，以确保它满足任何已配置的连接质量要求。 这可能包括优化漫游扫描、优化 AP 选择、优化关联进程，并最大限度地减少所需的安全握手。 在扫描过程中，如果设备需要找到的 BSS 条目的其他关联参数 (例如，PMKID 用于漫游) ，则它可以发送 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 关联 \_ 参数 \_ 请求](ndis-status-wdi-indication-association-parameters-request.md) 指示以获取参数。 如果可用，主机将使用 [OID \_ WDI \_ 设置 \_ 关联 \_ 参数](oid-wdi-set-association-parameters.md)来配置这些参数。

如果连接失败或被中止，则端口不应重置任何可能已在 connect 命令之外配置的设置。 它必须支持对同一端口发出第二次连接调用的主机。

在关联尝试结束时，必须由端口报告每个 BSS 条目的连接尝试的状态。 这包括成功的尝试以及任何失败的尝试。 无论何时，该端口都必须与不多个访问点或 Wi-fi Direct 中转关联。

当连接正在进行时，端口必须维护在其他端口上建立的任何连接 (例如，基础结构或 Wi-fi Direct) 。 但是，端口可能会减少向其他端口提供的中值访问以完成连接。 在连接期间，主机可以在其他端口上提交数据包发送请求。

如果用于连接的身份验证算法需要 802.1 x 端口授权才能进行网络访问，则主机会在关联操作成功完成后授权端口。

802.11 工作站使用 PMKID 缓存进行预身份验证，以访问已启用稳健安全网络关联 (RSNA) 身份验证算法的点。 如果802.11 工作站与提供 PMKID 的 BSSID 关联或重新关联，802.11 工作站必须使用 RSN 信息元素中的 PMKID 数据 (其关联或重新关联帧的 RSN IE) 。

如果端口在 [**WDI \_ TLV \_ 工作站 \_ 特性**](./wdi-tlv-station-attributes.md)中声明支持主机 FIPS 模式，则可以在连接参数中将 HostFIPSModeEnabled 设置为1。

如果 HostFIPSModeEnabled 设置为1，则适用以下规则。

-   该端口必须遵循在 FIPS 模式下发送操作中发送/接收数据帧和在 FIPS 模式下接收操作的指导原则。
-   此端口不得声明对发送到非 HT 访问点的关联请求中的任何 QoS 协议的支持。 超线程连接需要 QoS 支持。
-   该端口不得协商 TSpec，且不能执行传输 MSDU 聚合。
-   端口必须确保 SPP MSDU 支持的位 (位 10) 它所传输的 RSN 功能的位设置为零。 此模式仅支持 PP MSDU。

连接参数不能将 MFPEnabled 和 HostFIPSModeEnabled 都设置为1。 管理帧保护 (802.11 w) 要求使用端口对某些管理和操作帧进行加密/解密，因此无法使用主机 FIPS 模式为连接启用此功能。 此外，无线 LAN 唤醒功能在主机-FIPS 模式下不适用。

## <a name="task-parameters"></a>任务参数


| TLV                                                                      | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 连接 \_ 参数**](./wdi-tlv-connect-parameters.md) |                                |          | 连接参数。                                                                                                                                                                                                                                                                                                                                                                                   |
| [**WDI \_ TLV \_ 连接 \_ BSS \_ 条目**](./wdi-tlv-connect-bss-entry.md)  | X                              |          | 候选连接 BSS 条目的首选列表。 此端口应尝试连接到这些 BSS 条目，直到该列表已用尽或连接成功完成。 如果需要，此端口可以重新调整条目的优先级。 如果适配器设置了 "连接 BSS 选择替代位"，则它可以选择不在此列表中的 BSS，前提是它遵循允许/禁止列表。 |

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 连接 \_ 完成](ndis-status-wdi-indication-connect-complete.md)

## <a name="unsolicited-indication"></a>未经请求的指示

[NDIS \_ 状态 \_ WDI \_ 指示 \_ 关联 \_ 结果](ndis-status-wdi-indication-association-result.md)

[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

