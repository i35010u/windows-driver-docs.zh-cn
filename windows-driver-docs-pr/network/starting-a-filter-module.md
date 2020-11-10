---
title: 启动筛选器模块
description: 启动筛选器模块
ms.assetid: 493cb922-22bc-4845-b5a2-6f610559534d
keywords:
- 筛选器模块 WDK 网络，开始
- 正在启动筛选器模块
- 筛选器驱动程序 WDK 网络，启动筛选器模块
- NDIS 筛选器驱动程序 WDK，启动筛选器模块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1b81e92285f15fc655d40704e19c567cf54ad27
ms.sourcegitcommit: cfd4d8ee889c6a3feed79ae112662f6c095b6a36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94417451"
---
# <a name="starting-a-filter-module"></a>启动筛选器模块

为了启动暂停的筛选器模块，NDIS 调用筛选器驱动程序的 [*FilterSetModuleOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options) 函数（如果有），然后调用 [*FilterRestart*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart) 函数。 在 *FilterRestart* 函数中，筛选器模块将进入执行开始时的 *重新启动* 状态。

如果驱动程序提供了 [*FilterSetModuleOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options)的入口点，则驱动程序可以更改筛选器模块的部分特性。 有关详细信息，请参阅 [Data 旁路 Mode](data-bypass-mode.md)。

当它调用筛选器驱动程序的 [*FilterRestart*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)函数时，ndis 会将一个指针传递到 [**ndis \_ 重新启动 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)结构，以在 [**ndis \_ 筛选器 \_ 重新启动 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_restart_parameters)结构的 **RestartAttributes** 成员中筛选驱动程序。 筛选器驱动程序可以修改底层驱动程序指定的重新启动属性。 有关如何修改 restart 特性的详细信息，请参阅 *FilterRestart* 。

**注意** 在 NDIS 为堆栈中的任何筛选器模块调用 [*FilterRestart*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)函数之前，ndis 为堆栈中的所有筛选器模块调用 [*FilterSetModuleOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_set_module_options) 。

NDIS 作为即插即用操作的一部分启动筛选器模块以重新启动驱动程序堆栈。 有关重新启动驱动程序堆栈的概述，请参阅 [重新启动驱动程序堆栈](restarting-a-driver-stack.md)。

代表处于 *重新启动* 状态的筛选器模块，筛选器驱动程序：

- 完成重新启动正常发送和接收操作所需的任何操作。

    有关发送和接收操作的详细信息，请参阅 [筛选模块发送和接收操作](filter-module-send-and-receive-operations.md)。

- 可以读取或写入筛选器模块的可配置参数。

- 可以接收网络数据指示。 驱动程序可以复制并排队此类数据，并在以后将其指示到过量的驱动程序，也可以丢弃数据。

- 不应启动任何新的接收指示。

- 应通过调用 [**NdisFSendNetBufferListsComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)函数立即拒绝对其 [*FilterSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_send_net_buffer_lists)函数发出的所有新发送请求。 它应将每个 [网络 \_ 缓冲区 \_ 列表](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 中的完整状态设置为 "已 \_ 暂停 NDIS 状态" \_ 。

- 可以通过 [**NdisFIndicateStatus**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfindicatestatus) 函数提供状态指示。

    有关状态指示的详细信息，请参阅 [筛选模块状态指示](filter-module-status-indications.md)。

- 应在 [*FilterOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_oid_request) 函数中处理 OID 请求。

    有关 OID 请求的详细信息，请参阅 [筛选器模块 OID 请求](filter-module-oid-requests.md)。

- 不应启动任何新的发送请求。

- 应通过调用 [**NdisFReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreturnnetbufferlists) 函数立即将新的接收指示返回到 NDIS。 如有必要，驱动程序可以在返回之前复制此类接收指示。

- 可以向底层驱动程序发出 OID 请求，以设置或查询更新的配置信息。

- 应在其 [*FilterStatus*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status) 函数中处理状态指示。

- 应指示 NDIS \_ 状态 \_ 成功或失败状态。 如果筛选器模块未重启，NDIS 会将其分离，如果是必需的筛选器，NDIS 将终止整个驱动程序堆栈。

筛选器驱动程序成功重新启动发送和接收操作后，必须完成重新启动操作。 筛选器驱动程序可以通过返回 NDIS \_ 状态 \_ 成功或 \_ \_ 分别从 [*FilterRestart*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart)返回的 ndis 状态，来同步或异步完成重新启动操作。

如果驱动程序返回 NDIS \_ 状态 " \_ 挂起"，则必须在完成重启操作后调用 [**NdisFRestartComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfrestartcomplete) 函数。 在这种情况下，驱动程序将重启操作的最终状态传递到 **NdisFRestartComplete** 。

重新启动操作完成后，筛选器模块将处于 " *正在运行* " 状态。 驱动程序将恢复正常发送和接收处理。

当筛选器驱动程序处于 *重新启动* 状态时，NDIS 不会启动其他即插即用操作，如、附加、分离或暂停请求。 在筛选器驱动程序处于 *运行* 状态之后，NDIS 可以启动暂停请求。 有关暂停筛选器模块的详细信息，请参阅 [暂停筛选器模块](pausing-a-filter-module.md)。