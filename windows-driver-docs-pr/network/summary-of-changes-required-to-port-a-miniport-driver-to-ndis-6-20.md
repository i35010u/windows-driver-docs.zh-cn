---
title: 将微型端口驱动程序移植到 NDIS 6.20 的更改摘要
description: 将微型端口驱动程序移植到 NDIS 6.20 所要做出的更改摘要
ms.assetid: e52137ac-5333-4b62-8e26-686196d8ca78
keywords:
- NDIS 6.20 WDK，移植微型端口驱动程序
- 将微型端口驱动程序移植到 NDIS 6.20 WDK
- 微型端口驱动程序 WDK
- 微型端口驱动程序 WDK，移植到 NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c53b88f0889702b0b41f22cf0f205e77cac098a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841811"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-620"></a>将微型端口驱动程序移植到 NDIS 6.20 所要做出的更改摘要





本主题概述了将 NDIS 1.x 微型端口驱动程序移植到 NDIS 6.20 所需的更改。

NDIS 6.20 保持与早期的 NDIS 版本的向后兼容性。 有关向后兼容性的详细信息，请参阅[NDIS 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。

若要更新微型端口驱动程序以支持 NDIS 6.20 环境，必须按如下所示修改 NDIS 6. x 微型端口驱动程序：

<a href="" id="build-environment"></a>**生成环境**  
将预处理器定义 NDIS60 替换\_微型端口\_驱动程序或 NDIS61\_微型端口\_驱动程序与 NDIS620\_微型端口\_驱动程序。

<a href="" id="general-porting-requirements"></a>**一般移植要求**  
-   将过时的接口替换为 NDIS 6.20 版本。 有关过时接口的详细信息，请参阅[NDIS 6.20 中的过时接口](obsolete-interfaces-in-ndis-6-20.md)。

-   更新以下接口以支持超过64个处理器：

    -   接收方缩放（RSS）
    -   处理器信息设备驱动程序接口
    -   资源分配
    -   读取和写入锁

    有关支持超过64个处理器的详细信息，请参阅[NDIS 6.20 中对超过64个处理器的支持](support-for-more-than-64-processors-in-ndis-6-20.md)。

<a href="" id="driver-initialization"></a>**驱动程序初始化**  
-   将 ndis 版本设置为6.20 （在[**ndis\_微型\_驱动\_程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)的**MajorNdisVersion**和**MinorNdisVersion**成员中，将传递到[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)函数。

-   将 NDIS\_微型\_\_端口的**MajorDriverVersion**和**MinorDriverVersion**成员中的微型端口驱动程序版本设置为合适的特定于驱动程序的值。

-   在 NDIS\_微型端口\_驱动程序\_特征结构中定义直接 OID 请求入口点。 对于 NDIS 6.1 驱动程序，对直接 OID 请求接口的支持是可选的，但对于 NDIS 6.20 驱动程序则是必需的。 有关微型端口驱动程序直接 OID 请求接口的详细信息，请参阅[微型端口适配器 OID 请求](miniport-adapter-oid-requests.md)。

<a href="" id="miniport-adapter-initialization"></a>**微型端口适配器初始化**  
-   使用最新版本的微型端口适配器功能播发接口。 以下接口具有更新的功能：
    -   电源管理
    -   接收方缩放（RSS）
    -   硬件协助（VMQ）
-   使用这些结构的更新版本：

    -   [**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)
    -   [**NDIS\_RESTART\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)
    -   [**NDIS\_接收\_刻度\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)
    -   [**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

    有关 NDIS 结构版本信息的信息，请参阅[指定 Ndis 版本信息](specifying-ndis-version-information.md)。

<a href="" id="send-and-receive-code-paths"></a>**发送和接收代码路径**  
-   NDIS 6.20 驱动程序必须支持在处理接收中断时接收方限制（RST）。 [*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)和[*MiniportMessageInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc) DPC 处理程序函数的*RECEIVETHROTTLEPARAMETERS*参数指向[**NDIS\_接收\_控制器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_throttle_parameters)结构。 进入延迟的过程调用（DPC）处理程序时，NDIS\_接收\_控制器的**MaxNblsToIndicate**成员\_参数结构指定最大[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)数小型端口驱动程序应在 DPC 中指示的结构。 有关 RST 的详细信息，请参阅[NDIS 6.20 中的接收方限制](receive-side-throttle-in-ndis-6-20.md)。

-   使用[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的更新版本。

-   （可选）支持虚拟机队列（VMQ）接口。 有关 VMQ 的详细信息，请参阅[NDIS 6.20 中的虚拟机队列（VMQ）](virtual-machine-queue--vmq--in-ndis-6-20.md)。

 

 





