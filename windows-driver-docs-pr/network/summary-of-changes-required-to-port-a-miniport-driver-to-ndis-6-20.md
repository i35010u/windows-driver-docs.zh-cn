---
title: 若要移植到 NDIS 6.20 的微型端口驱动程序的更改摘要
description: 将微型端口驱动程序移植到 NDIS 6.20 所要做出的更改摘要
ms.assetid: e52137ac-5333-4b62-8e26-686196d8ca78
keywords:
- NDIS 6.20 WDK，移植微型端口驱动程序
- 移植到 NDIS 6.20 WDK 的微型端口驱动程序
- 微型端口驱动程序 WDK
- 微型端口驱动程序 WDK，移植到 NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04461247d1e2de053a49944bee8437e27c2b413f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366361"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-620"></a>将微型端口驱动程序移植到 NDIS 6.20 所要做出的更改摘要





本主题总结了要移植到 NDIS 6.20 NDIS 6.x 微型端口驱动程序所需的更改。

NDIS 6.20 保留与早期 NDIS 版本的向后兼容性。 有关向后兼容性的详细信息，请参阅[NDIS 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。

若要更新的微型端口驱动程序来支持 NDIS 6.20 环境，必须按如下所示修改 NDIS 6.x 微型端口驱动程序：

<a href="" id="build-environment"></a>**构建环境**  
替换为预处理器定义 NDIS60\_微型端口\_驱动程序或 NDIS61\_微型端口\_驱动程序和 NDIS620\_微型端口\_驱动程序。

<a href="" id="general-porting-requirements"></a>**移植的一般要求**  
-   使用 NDIS 6.20 版本替换已过时的接口。 有关已过时的接口的详细信息，请参阅[NDIS 6.20 中已过时接口](obsolete-interfaces-in-ndis-6-20.md)。

-   更新了以下接口来支持超过 64 个处理器：

    -   接收方缩放 (RSS)
    -   处理器信息设备驱动程序接口
    -   资源分配
    -   读取和写入锁

    支持超过 64 个处理器的详细信息，请参阅[支持多个 64 位处理器中 NDIS 6.20](support-for-more-than-64-processors-in-ndis-6-20.md)。

<a href="" id="driver-initialization"></a>**驱动程序初始化**  
-   将 NDIS 版本设置为在 6.20 **MajorNdisVersion**并**MinorNdisVersion**的成员[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958)结构，它传递给[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)函数。

-   在中设置的微型端口驱动程序版本**MajorDriverVersion**并**MinorDriverVersion** NDIS 成员\_微型端口\_驱动程序\_特征为适当的驱动程序特定值的结构。

-   定义直接 OID 请求入口点在 NDIS\_微型端口\_驱动程序\_特征结构。 支持直接的 OID 请求接口是可选的 NDIS 6.1 驱动程序，但必须为 NDIS 6.20 驱动程序。 微型端口驱动程序直接 OID 请求接口的详细信息，请参阅[微型端口适配器 OID 请求](miniport-adapter-oid-requests.md)。

<a href="" id="miniport-adapter-initialization"></a>**微型端口适配器初始化**  
-   使用最新版本的微型端口适配器功能播发接口。 以下接口已经更新功能：
    -   电源管理
    -   接收方缩放 (RSS)
    -   硬件协助 (VMQ)
-   使用这些结构的更新的版本：

    -   [**NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)
    -   [**NDIS\_RESTART\_GENERAL\_ATTRIBUTES**](https://msdn.microsoft.com/library/windows/hardware/ff567260)
    -   [**NDIS\_RECEIVE\_SCALE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff567228)
    -   [**NDIS\_微型端口\_适配器\_硬件\_帮助\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565924)

    NDIS 结构版本信息有关的信息，请参阅[指定 NDIS 版本信息](specifying-ndis-version-information.md)。

<a href="" id="send-and-receive-code-paths"></a>**发送和接收的代码路径**  
-   NDIS 6.20 驱动程序必须支持接收方在处理过程中的限制 (RST) 接收中断。 *ReceiveThrottleParameters*的参数[ *MiniportInterruptDPC* ](https://msdn.microsoft.com/library/windows/hardware/ff559398)并[ *MiniportMessageInterruptDPC* ](https://msdn.microsoft.com/library/windows/hardware/ff559411) DPC 处理程序函数依次指向[ **NDIS\_接收\_限制\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff567241)结构。 在延缓的过程调用 (DPC) 处理程序中，进入**MaxNblsToIndicate**成员的 NDIS\_接收\_限制\_参数结构指定的最大数目[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)微型端口驱动程序应指示 DPC 中的结构。 RST 的详细信息，请参阅[接收端限制在 NDIS 6.20](receive-side-throttle-in-ndis-6-20.md)。

-   使用的更新的版本[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。

-   选择性地支持虚拟机队列 (VMQ) 接口。 有关 VMQ 的详细信息，请参阅[虚拟机队列 (VMQ) 在 NDIS 6.20](virtual-machine-queue--vmq--in-ndis-6-20.md)。

 

 





