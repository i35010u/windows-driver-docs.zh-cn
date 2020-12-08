---
title: 将微型端口驱动程序移植到 NDIS 6.20 的更改摘要
description: 将微型端口驱动程序移植到 NDIS 6.20 所要做出的更改摘要
keywords:
- NDIS 6.20 WDK，移植微型端口驱动程序
- 将微型端口驱动程序移植到 NDIS 6.20 WDK
- 微型端口驱动程序 WDK
- 微型端口驱动程序 WDK，移植到 NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e783885b985fed2c1f3d6a1d14b0c107472949b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824975"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-620"></a>将微型端口驱动程序移植到 NDIS 6.20 所要做出的更改摘要





本主题概述了将 NDIS 1.x 微型端口驱动程序移植到 NDIS 6.20 所需的更改。

NDIS 6.20 保持与早期的 NDIS 版本的向后兼容性。 有关向后兼容性的详细信息，请参阅 [NDIS 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。

若要更新微型端口驱动程序以支持 NDIS 6.20 环境，必须按如下所示修改 NDIS 6. x 微型端口驱动程序：

<a href="" id="build-environment"></a>**生成环境**  
将预处理器定义 NDIS60 \_ 微型端口 \_ 驱动程序或 NDIS61 微型端口驱动程序替换 \_ \_ 为 NDIS620 \_ 微型端口驱动 \_ 程序。

<a href="" id="general-porting-requirements"></a>**一般移植要求**  
-   将过时的接口替换为 NDIS 6.20 版本。 有关过时接口的详细信息，请参阅 [NDIS 6.20 中的过时接口](obsolete-interfaces-in-ndis-6-20.md)。

-   更新以下接口以支持超过64个处理器：

    -   接收方缩放 (RSS) 
    -   处理器信息设备驱动程序接口
    -   资源分配
    -   读取和写入锁

    有关支持超过64个处理器的详细信息，请参阅 [NDIS 6.20 中对超过64个处理器的支持](support-for-more-than-64-processors-in-ndis-6-20.md)。

<a href="" id="driver-initialization"></a>**驱动程序初始化**  
-   将 ndis 版本设置为6.20，并将 [**ndis \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构传递到 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数的 **MajorNdisVersion** 和 **MinorNdisVersion** 成员。

-   将 NDIS 微型端口驱动程序特征结构的 **MajorDriverVersion** 和 **MinorDriverVersion** 成员中的微型端口驱动程序版本设置 \_ \_ \_ 为合适的特定于驱动程序的值。

-   在 NDIS \_ 微型端口 \_ 驱动程序特征结构中定义直接 OID 请求入口点 \_ 。 对于 NDIS 6.1 驱动程序，对直接 OID 请求接口的支持是可选的，但对于 NDIS 6.20 驱动程序则是必需的。 有关微型端口驱动程序直接 OID 请求接口的详细信息，请参阅 [微型端口适配器 OID 请求](miniport-adapter-oid-requests.md)。

<a href="" id="miniport-adapter-initialization"></a>**微型端口适配器初始化**  
-   使用最新版本的微型端口适配器功能播发接口。 以下接口具有更新的功能：
    -   电源管理
    -   接收方缩放 (RSS) 
    -   硬件协助 (VMQ) 
-   使用这些结构的更新版本：

    -   [**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)
    -   [**NDIS \_ 重新启动 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)
    -   [**NDIS \_ 接收 \_ 刻度 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)
    -   [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

    有关 NDIS 结构版本信息的信息，请参阅 [指定 Ndis 版本信息](specifying-ndis-version-information.md)。

<a href="" id="send-and-receive-code-paths"></a>**发送和接收代码路径**  
-   NDIS 6.20 驱动程序必须支持接收方限制 (RST) 处理接收中断。 [*MiniportInterruptDPC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)和 [*MiniportMessageInterruptDPC*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc) DPC 处理程序函数的 *ReceiveThrottleParameters* 参数指向 [**NDIS \_ 接收 \_ 调节 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_throttle_parameters)结构。 进入延迟的过程调用 (DPC) 处理程序时，NDIS **MaxNblsToIndicate** \_ 接收 \_ 调节参数结构的 MaxNblsToIndicate 成员 \_ 指定了微型端口驱动程序在 DPC 中应显示的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构的最大数目。 有关 RST 的详细信息，请参阅 [NDIS 6.20 中的接收方限制](receive-side-throttle-in-ndis-6-20.md)。

-   使用 [**NET \_ BUFFER**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer) 结构的更新版本。

-   （可选）支持虚拟机队列 (VMQ) 接口。 有关 VMQ 的详细信息，请参阅 [NDIS 6.20 中的虚拟机队列 (VMQ) ](virtual-machine-queue--vmq--in-ndis-6-20.md)。

 

