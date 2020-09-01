---
title: OID_TCP_TASK_OFFLOAD
description: 本主题介绍) OID_TCP_TASK_OFFLOAD 对象标识符 (OID。
ms.assetid: 4e16cdb7-b899-43b6-a94b-d691622be105
keywords:
- OID_TCP_TASK_OFFLOAD
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4350c7d874f6fe10d4db38eb9e7421bd5ce12039
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215829"
---
# <a name="oid_tcp_task_offload"></a>OID_TCP_TASK_OFFLOAD

宿主堆栈会查询 OID_TCP_TASK_OFFLOAD OID，以获取微型端口驱动程序的 NIC 或卸载目标的 TCP 卸载功能。 确定 NIC 或卸载目标支持的卸载功能之后，主机堆栈会将此 OID 设置为启用一个或多个报告的功能。 主机堆栈还可以通过设置 OID_TCP_TASK_OFFLOAD 来禁用 NIC 或卸载目标的 TCP 卸载功能。 一次只能有一个协议可以启用特定 NIC 的 TCP 卸载功能。

## <a name="querying-offload-capabilities"></a>查询卸载功能

当宿主堆栈查询 OID_TCP_TASK_OFFLOAD 时，它会在 *InformationBuffer* 中提供 [NDIS_TASK_OFFLOAD_HEADER](/previous-versions/windows/hardware/network/ff559004(v=vs.85)) 结构。 此结构指定以下各项：

- 宿主堆栈支持的卸载版本。
- 主机堆栈处理的发送和接收数据包的封装格式。
- 此类数据包中封装标头的大小。

使用此信息，微型端口驱动程序或其 NIC 可以定位传输数据包中第一个 IP 标头的开头，这是执行卸载任务的先决条件。 卸载目标需要知道封装格式才能处理接收数据包。 为了响应 OID_TCP_TASK_OFFLOAD 的查询，微型端口驱动程序或卸载目标将在 *InformationBuffer*中返回，后跟一个或多个 [NDIS_TASK_OFFLOAD](/previous-versions/windows/hardware/network/ff558995(v=vs.85)) 结构的 NDIS_TASK_OFFLOAD_HEADER 结构。 每个 NDIS_TASK_OFFLOAD 结构描述了微型端口驱动程序 NIC 或卸载目标支持的卸载功能。 如果微型端口驱动程序的 NIC 或卸载目标支持多个版本的特定卸载功能，则它应为每个版本返回一个 NDIS_TASK_OFFLOAD 结构。

每个 NDIS_TASK_OFFLOAD 结构都有一个 **任务** 成员，该成员指定结构应用于的特定卸载功能。 每个 NDIS_TASK_OFFLOAD 结构还包含 **TaskBuffer** ，其中包含与指定的卸载功能有关的信息。 **TaskBuffer**中的信息设置为以下结构之一：

- [NDIS_TASK_TCP_IP_CHECKSUM](/previous-versions/windows/hardware/network/ff559004(v=vs.85))  
    指定校验和卸载功能。
- [NDIS_TASK_IPSEC](/previous-versions/windows/hardware/network/ff558990(v=vs.85))  
    指定 (IPsec) 卸载功能的 Internet 协议安全性。
- [NDIS_TASK_TCP_LARGE_SEND](/previous-versions/windows/hardware/network/ff559008(v=vs.85))  
    指定大 TCP 数据包分段功能。
- [NDIS_TASK_TCP_CONNECTION_OFFLOAD](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_ndis_tcp_connection_offload_parameters)  
    指定 TCP 烟囱卸载功能。 有关 NDIS_TASK_TCP_CONNECTION_OFFLOAD 的详细信息，请参阅 [TCP 烟囱卸载](/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)。

> [!NOTE]
> 如果中间驱动程序修改转发到基础微型端口驱动程序的数据包的内容，以便无法对数据包执行 TCP 卸载功能，则中间驱动程序应使用 NDIS_STATUS_NOT_SUPPORTED 状态对 OID_TCP_TASK_OFFLOAD 查询进行响应，而不是将 OID 请求传递到基础微型端口驱动程序或卸载目标。

## <a name="enabling-offload-capabilities"></a>启用卸载功能

在查询 NIC 或卸载目标的卸载功能之后，主机堆栈通过设置 OID_TCP_TASK_OFFLOAD 来启用一个或多个此类功能。 设置 OID_TCP_TASK_OFFLOAD 时，主机堆栈提供 *InformationBuffer*中的 NDIS_TASK_OFFLOAD_HEADER 结构，其后紧跟主机堆栈正在启用的每个卸载功能的 NDIS_TASK_OFFLOAD 结构。

每个 NDIS_TASK_OFFLOAD 结构中的 **任务** 指示宿主堆栈正在启用的卸载功能。 宿主堆栈还通过设置每个 NDIS_TASK_OFFLOAD 结构的 **TaskBuffer** 中结构的成员来启用特定卸载功能的特定方面。

## <a name="changing-offload-capabilities"></a>更改卸载功能 

若要更改为 NIC 或卸载目标启用的卸载功能，主机堆栈会将设置 OID_TCP_TASK_OFFLOAD。 微型端口驱动程序或卸载目标必须仅启用由最新的一组 OID_TCP_TASK_OFFLOAD 指定的卸载功能。 微型端口驱动程序或卸载目标必须禁用所有其他卸载功能。 请注意，在禁用特定 TCP 烟囱卸载功能之前，主机堆栈终止使用该功能的任何已卸载的 TCP 连接的卸载。

卸载目标可以使用 "暂停" 或 "恢复卸载" 指示更改其报告的 TCP 卸载功能：

- 卸载目标通过调用 [NdisMIndicateStatusEx](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 函数，并将 NDIS_STATUS_INDICATION >**StatusCode** 成员设置为 NDIS_STATUS_OFFLOAD_PAUSE 来进行暂停指示。
- 卸载目标通过调用 **NdisMIndicateStatusEx** 函数并将 NDIS_STATUS_INDICATION >**StatusCode** 成员设置为 NDIS_STATUS_OFFLOAD_RESUME 来进行恢复指示。

在卸载目标请求宿主堆栈恢复卸载状态对象之后，主机堆栈再次查询 OID_TCP_TASK_OFFLOAD 以获取卸载目标的 TCP 卸载修改后的功能。 有关详细信息，请参阅 [NDIS_STATUS_OFFLOAD_RESUME](./index.md)。

## <a name="disabling-offload-capabilities"></a>禁用卸载功能

若要禁用 NIC 或卸载目标支持的所有卸载功能，主机堆栈会将 OID_TCP_TASK_OFFLOAD 设置。 在 *InformationBuffer*中，主机堆栈提供 NDIS_TASK_OFFLOAD_HEADER 结构，此结构的 **OffsetFirstTask** 成员设置为零。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 