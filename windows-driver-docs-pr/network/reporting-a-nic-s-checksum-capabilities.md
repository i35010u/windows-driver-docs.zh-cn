---
title: 报告 NIC 的校验和功能
description: 报告 NIC 的校验和功能
keywords:
- 任务卸载 WDK TCP/IP 传输，校验和任务
- 校验和任务 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76029e55e37e1c943a0f836628daaa9e31e6e53e
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102247779"
---
# <a name="reporting-a-nics-checksum-capabilities"></a>报告 NIC 的校验和功能





NDIS 微型端口驱动程序报告 NIC 当前是否配置为在 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload) 结构中计算和验证 IP、TCP 和 UDP 校验和。 微型端口驱动程序必须在 [**NDIS \_ 微型端口 \_ 适配器 \_ 卸载 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_offload_attributes) 结构中包含当前校验和卸载配置。 微型端口驱动程序从 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数，并传入 NDIS \_ 微型端口 \_ 适配器 \_ 卸载特性中的信息 \_ 。

微型端口驱动程序必须在 [**NDIS \_ 状态 \_ 任务 " \_ 卸载 \_ 当前 \_ 配置**](./ndis-status-task-offload-current-config.md) 状态指示" 中报告当前校验和卸载配置中的更改（如果有）。

为了响应 [OID \_ tcp \_ 卸载的 \_ 当前 \_ 配置](./oid-tcp-offload-current-config.md)查询，ndis 在 ndis \_ OID 请求结构的 InformationBuffer 成员中包含 ndis tcp \_ IP \_ 校验和 \_ 卸载结构。 [**\_**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload) [**\_ \_**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)  NDIS 使用微型端口驱动程序提供的信息。

微型端口驱动程序指示 IPv4 和 IPv6 发送和接收数据包的以下校验和信息：

-   校验和类型 (IP、TCP 或 UDP) NIC 可为发送数据包计算，并可验证接收数据包。

-   封装设置，位于 **封装** 成员中。 有关此成员的详细信息，请参阅 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)中的 "备注" 部分。

-   NIC 是否可以计算或验证 (或计算和验证 IP 标头包含 IPv4 选项的数据包) 校验和。

-   NIC 是否可以计算或验证 (或计算和验证 IP 标头包含 IPv6 扩展标头的 IPv6 数据包的) 校验和。

-   NIC 是否可以计算或验证 (或计算和验证 TCP 标头包含 TCP 选项的数据包) 校验和。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

