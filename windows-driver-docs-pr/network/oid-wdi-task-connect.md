---
title: OID_WDI_TASK_CONNECT
description: IHV 组件连接到一个访问点或 Wi-Fi Direct 转 OID_WDI_TASK_CONNECT 请求。
ms.assetid: 63ba3979-6b30-49bf-91a9-fa01f0ef4922
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_CONNECT 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 8526e4ea1afb6b5db683ff0dc669d55116cb4a82
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348849"
---
# <a name="oidwditaskconnect"></a>OID\_WDI\_TASK\_CONNECT


OID\_WDI\_任务\_IHV 组件连接到一个访问点或 Wi-Fi Direct 转的 CONNECT 请求。

| Object | 中止支持                                     | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 中止后面必须跟 dot11 重置。 | 4                                     | 10                              |

 

作为连接的一部分，IHV 组件必须与同步，进行身份验证，并将关联到 BSS。 主机提供 IHV 组件可以尝试连接到的 BSS 条目。 一旦 IHV 组件已成功连接到这些条目之一，它应完成连接过程。 如果无法连接到任何 BSS 条目，它应完成与失败的连接过程。

IHV 组件不需要执行扫描以查找 BSS 条目的候选者。 它可以使用由主机提供的连接的列表。 它可以尝试连接到每个，一个接一个。 主机排序 RSSI，通过网络但 IHV 组件可以使用其自己的连接的顺序。 如果适配器没有指定"连接 BSS 选择替代"，它必须仅使用由主机提供的连接的条目。 主机可能会发出中止在未完成连接。 接收中止后，该端口必须结束连接尝试并报告已完成到主机。

如果适配器指定"连接 BSS 选择替代"，它可以在其自己查找候选者 BSS 项上执行扫描。 它可以连接到任何 BSS 条目找到，只要它满足主机配置的参数。 它应优化此选择，以确保其满足任何配置的连接质量要求。 这可能包括优化漫游扫描、 优化 AP 选择、 优化关联过程和最大程度减少所需的安全握手。 在扫描期间如果设备需要其他关联参数来保存找到的 BSS 条目 (例如，PMKID 漫游)，它可以发送[NDIS\_状态\_WDI\_指示\_关联\_参数\_请求](ndis-status-wdi-indication-association-parameters-request.md)表示要获取的参数。 如果可用，请在主机配置这些参数与[OID\_WDI\_设置\_关联\_参数](oid-wdi-set-association-parameters.md)。

如果连接失败或被中止，该端口不应重置配置 connect 命令之外的任何设置。 它必须支持主机发出的同一端口上的第二个连接调用。

必须通过关联尝试末尾处的端口报告为每个 BSS 条目连接尝试的状态。 这包括成功的尝试，并且还任何失败的尝试。 在任何时候，该端口必须与多个访问点或 Wi-Fi Direct 转相关联。

正在进行连接时，该端口必须维护 （例如，基础结构或 Wi-Fi Direct） 的其他端口上建立任何连接。 但是，端口可能会降低的中等的访问权限提供给要完成连接的其他端口。 在连接中，主机可以提交其他端口上的数据包发送请求。

如果用于连接的身份验证算法要求 802.1 x 端口授权进行网络访问权限，请在主机可授权端口后关联操作已成功完成。

802.11 工作站使用 PMKID 缓存进行预身份验证来访问已启用可靠安全网络关联 (RSNA) 身份验证算法的点。 如果将关联或重新关联到具有提供的 PMKID BSSID 802.11 工作站，802.11 工作站必须使用 PMKID 数据及其关联或重新关联的帧的 RSN 信息元素 (RSN IE) 中。

如果端口声明中的主机 FIPS 模式的支持[ **WDI\_TLV\_工作站\_特性**](https://msdn.microsoft.com/library/windows/hardware/dn898066)，HostFIPSModeEnabled 可能设置为 1 的连接参数。

如果 HostFIPSModeEnabled 设置为 1，以下规则适用。

-   端口必须遵循的准则在 FIPS 模式下的发送操作和在 FIPS 模式下的接收操作中的发送/接收数据帧。
-   该端口不得声明对关联请求发送到的非超线程访问点中任何 QoS 协议的支持。 QoS 支持是超线程连接所必需的。
-   端口必须不协商 TSpec，并且必须执行传输 MSDU 聚合。
-   端口必须确保它能够位 （位 10） 的 RSN 功能 IE 传输设置为零 SPP A MSDU。 在此模式下支持仅 PP A-MSDU。

连接参数不能同时设置为 1 的 MFPEnabled 和 HostFIPSModeEnabled。 管理框架保护 (802.11w) 需要端口以使它不能为使用主机 FIPS 模式下的连接启用加密/解密特定的管理和操作帧。 此外，唤醒无线 LAN 功能不在主机 FIPS 模式下适用。

## <a name="task-parameters"></a>任务参数


| TLV                                                                      | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                                                                                                                                                                                                                                                                                                  |
|--------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_CONNECT\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/dn926266) |                                |          | 连接参数。                                                                                                                                                                                                                                                                                                                                                                                   |
| [**WDI\_TLV\_CONNECT\_BSS\_条目**](https://msdn.microsoft.com/library/windows/hardware/dn926264)  | X                              |          | 首选的候选项列表连接 BSS 条目。 端口应尝试连接到任何这些 BSS 条目，直到列表用完或已成功完成的连接。 如果需要该端口可以重新调整条目。 如果适配器设置连接 BSS 选择重写位，它可以选择不在此列表中，只要遵循允许/不允许列表 BSS。 |

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_CONNECT\_完成](ndis-status-wdi-indication-connect-complete.md)

## <a name="unsolicited-indication"></a>未经请求的指示

[NDIS\_状态\_WDI\_指示\_关联\_结果](ndis-status-wdi-indication-association-result.md)

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
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




