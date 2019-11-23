---
title: 将协议驱动程序移植到 NDIS 6.20 的更改摘要
description: 将协议驱动程序移植到 NDIS 6.20 所要做出的更改摘要
ms.assetid: d47b29a5-3385-4023-b94c-5cfbc225f48a
keywords:
- NDIS 6.20 WDK，移植协议驱动程序
- 将协议驱动程序移植到 NDIS 6.20 WDK
- 协议驱动程序 WDK
- 协议驱动程序 WDK，移植到 NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d2ac9d353afbdc943a98cbe53e1b4a2aba3462e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841806"
---
# <a name="summary-of-changes-required-to-port-a-protocol-driver-to-ndis-620"></a>将协议驱动程序移植到 NDIS 6.20 所要做出的更改摘要





本主题概述了移植 NDIS 6 所需的更改。*x*协议驱动程序到 NDIS 6.20。

NDIS 6.20 保持与早期的 NDIS 版本的向后兼容性。 有关向后兼容性的详细信息，请参阅[NDIS 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。

若要更新协议驱动程序以支持 NDIS 6.20 环境，必须按如下所示修改 NDIS 1.x 协议驱动程序：

<a href="" id="build-environment-------"></a>**生成环境**   
将预处理器定义 NDIS61 或 NDIS60 替换为 NDIS620。

<a href="" id="general-porting-requirements-------"></a>**一般移植要求**   
-   将过时的接口替换为 NDIS 6.20 版本。 有关过时接口的详细信息，请参阅[NDIS 6.20 中的过时接口](obsolete-interfaces-in-ndis-6-20.md)。

-   更新以下接口以支持超过64个处理器：

    -   接收方缩放（RSS）
    -   处理器信息设备驱动程序接口
    -   资源分配
    -   读取和写入锁

    有关支持超过64个处理器的详细信息，请参阅[NDIS 6.20 中对超过64个处理器的支持](support-for-more-than-64-processors-in-ndis-6-20.md)。

<a href="" id="driver-initialization-------"></a>**驱动程序初始化**   
-   将 ndis 版本设置为**6.20，** [ **\_协议\_驱动程序\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_protocol_driver_characteristics)结构传递到[**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)函数。

-   将 NDIS\_协议\_驱动程序\_特征结构的**MajorDriverVersion**和**MinorDriverVersion**成员中的协议驱动程序版本设置为合适的特定于驱动程序的值。

<a href="" id="protocol-bind-and-unbind-operations-------"></a>**协议绑定和取消绑定操作**   
-   使用最新版本的微型端口适配器功能播发接口。 以下接口具有更新的功能：
    -   电源管理
    -   电源管理
    -   接收方缩放（RSS）
    -   硬件协助（VMQ）
-   使用这些结构的更新版本：

    -   [ **\_绑定\_参数的 NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)
    -   [**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

    有关 NDIS 结构版本信息的信息，请参阅[指定 Ndis 版本信息](specifying-ndis-version-information.md)。

<a href="" id="send-and-receive-data-paths-------"></a>**发送和接收数据路径**   
-   使用[**NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)结构的更新版本。

-   （可选）支持虚拟机队列（VMQ）接口。 有关 VMQ 的详细信息，请参阅[NDIS 6.20 中的虚拟机队列（VMQ）](virtual-machine-queue--vmq--in-ndis-6-20.md)。

 

 





