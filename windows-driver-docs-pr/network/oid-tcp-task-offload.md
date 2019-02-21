---
title: OID_TCP_TASK_OFFLOAD
description: 本主题介绍 OID_TCP_TASK_OFFLOAD 对象标识符 (OID)。
ms.assetid: 4e16cdb7-b899-43b6-a94b-d691622be105
keywords:
- OID_TCP_TASK_OFFLOAD
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89d1bb66da0b8a06997f4b619514cce89fe514f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526291"
---
# <a name="oidtcptaskoffload"></a>OID_TCP_TASK_OFFLOAD

主机堆栈查询 OID_TCP_TASK_OFFLOAD OID 获取 TCP 卸载功能的微型端口驱动程序的 NIC 或卸载目标。 在确定 NIC 或卸载目标支持的卸载功能之后, 主机堆栈设置此 OID 启用一个或多个报告功能。 所有的 NIC，也可以禁用主机堆栈或卸载目标的 TCP 通过设置 OID_TCP_TASK_OFFLOAD 卸载功能。 一次只有一个协议可以启用 TCP 卸载功能的特定 nic。

## <a name="querying-offload-capabilities"></a>查询卸载功能

当主机堆栈查询 OID_TCP_TASK_OFFLOAD 时，它会提供在*InformationBuffer* [NDIS_TASK_OFFLOAD_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff559004)结构。 此结构有如下规定：

- 由主机堆栈支持卸载版本。
- 为封装格式发送和接收数据包由主机堆栈处理。
- 此类数据包封装标头的大小。

使用此信息，微型端口驱动程序或其 NIC 可以传输数据包，这是用于执行卸载任务的先决条件中找到第一个 IP 标头的开头。 卸载目标需要知道到封装格式进程接收数据包。 OID_TCP_TASK_OFFLOAD 的查询响应，微型端口驱动程序或卸载目标返回时，在*InformationBuffer*，NDIS_TASK_OFFLOAD_HEADER 结构后面紧跟一个或多个[NDIS_TASK_卸载](https://msdn.microsoft.com/library/windows/hardware/ff558995)结构。 每个 NDIS_TASK_OFFLOAD 结构描述的微型端口驱动程序的 NIC 或卸载目标支持的卸载功能。 如果微型端口驱动程序的 NIC 或卸载目标支持多个版本的特定卸载功能，则它应返回一个 NDIS_TASK_OFFLOAD 结构为每个版本。

每个 NDIS_TASK_OFFLOAD 结构已**任务**成员，用于指定特定卸载的功能结构取决于。 每个 NDIS_TASK_OFFLOAD 结构还有**TaskBuffer** ，其中包含与指定的卸载功能相关的信息。 中的信息**TaskBuffer**格式化为一个以下结构：

- [NDIS_TASK_TCP_IP_CHECKSUM](https://msdn.microsoft.com/library/windows/hardware/ff559004)  
    指定校验和卸载功能。
- [NDIS_TASK_IPSEC](https://msdn.microsoft.com/library/windows/hardware/ff558990)  
    指定 Internet 协议安全 (IPsec) 卸载功能。
- [NDIS_TASK_TCP_LARGE_SEND](https://msdn.microsoft.com/library/windows/hardware/ff559008)  
    指定大型 TCP 数据包分段功能。
- [NDIS_TASK_TCP_CONNECTION_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff567873)  
    指定 TCP 烟囱卸载功能。 NDIS_TASK_TCP_CONNECTION_OFFLOAD 的详细信息，请参阅[TCP 烟囱卸载](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)。

> [!NOTE]
> 如果中间驱动程序修改以便 TCP 卸载函数不能执行的数据包转发到基础的微型端口驱动程序的数据包的内容，中间驱动程序应响应状态为 OID_TCP_TASK_OFFLOAD 查询而不是传递 OID NDIS_STATUS_NOT_SUPPORTED 对基础微型端口驱动程序的请求，或卸载目标。

## <a name="enabling-offload-capabilities"></a>启用卸载功能

查询的 NIC 或卸载目标后卸载功能，主机堆栈通过设置 OID_TCP_TASK_OFFLOAD 启用一个或多个这些功能。 当设置 OID_TCP_TASK_OFFLOAD，主机堆栈提供，请在*InformationBuffer*，NDIS_TASK_OFFLOAD_HEADER 结构后面紧随每个卸载功能的 NDIS_TASK_OFFLOAD 结构的主机启用堆栈。

**任务**结构中每个 NDIS_TASK_OFFLOAD 指示主机堆栈启用卸载功能。 主机还堆栈的启用特定方面的特定卸载功能，通过设置中的结构的成员**TaskBuffer**的每个 NDIS_TASK_OFFLOAD 结构。

## <a name="changing-offload-capabilities"></a>更改卸载功能 

若要更改为 NIC 或卸载目标启用卸载功能，主机堆栈设置 OID_TCP_TASK_OFFLOAD。 只有那些卸载指定的最新的 OID_TCP_TASK_OFFLOAD 集的功能，必须启用微型端口驱动程序或卸载目标。 微型端口驱动程序或卸载目标必须禁用所有其他卸载功能。 请注意，然后再禁用特定的 TCP 烟囱卸载功能，主机堆栈终止任何使用该功能的卸载 TCP 连接的卸载。

卸载目标可以使用暂停或恢复将卸载指示若要更改其报告的 TCP 卸载功能：

- 卸载目标调用，从而使暂停指示[NdisMIndicateStatusEx](https://msdn.microsoft.com/library/windows/hardware/ff563600) NDIS_STATUS_INDICATION 配合->**StatusCode**成员设置为 NDIS_STATUS_OFFLOAD_PAUSE。
- 卸载目标调用，从而使恢复指示**NdisMIndicateStatusEx** NDIS_STATUS_INDICATION 配合->**StatusCode**成员设置为 NDIS_STATUS_OFFLOAD_RESUME。

卸载目标请求主机堆栈继续卸载状态对象后，主机堆栈查询 OID_TCP_TASK_OFFLOAD 再次以获取卸载目标的 TCP 卸载修订后的功能。 有关详细信息，请参阅[NDIS_STATUS_OFFLOAD_RESUME](https://msdn.microsoft.com/library/windows/hardware/ff567405)。

## <a name="disabling-offload-capabilities"></a>禁用卸载功能

若要禁用所有支持的 NIC 或卸载目标的卸载功能，主机堆栈设置 OID_TCP_TASK_OFFLOAD。 在中*InformationBuffer*，主机堆栈提供具有 NDIS_TASK_OFFLOAD_HEADER 结构**OffsetFirstTask**此结构的成员设置为零。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 版本 | Windows Vista 及更高版本 |
| 标头 | Ntddndis.h （包括 Ndis.h） |

