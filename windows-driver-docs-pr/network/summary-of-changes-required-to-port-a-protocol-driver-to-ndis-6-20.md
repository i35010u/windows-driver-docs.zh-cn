---
title: 若要移植到 NDIS 6.20 协议驱动程序的更改摘要
description: 若要移植到 NDIS 6.20 协议驱动程序所需的更改的摘要
ms.assetid: d47b29a5-3385-4023-b94c-5cfbc225f48a
keywords:
- NDIS 6.20 WDK，移植协议驱动程序
- 移植到 NDIS 6.20 WDK 协议驱动程序
- 协议驱动程序 WDK
- 协议驱动程序 WDK，移植到 NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deed1d77b98591e6be28971a09e706d601647c9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534245"
---
# <a name="summary-of-changes-required-to-port-a-protocol-driver-to-ndis-620"></a>若要移植到 NDIS 6.20 协议驱动程序所需的更改的摘要





本主题概述了所需端口 NDIS 6 的更改。*x*到 NDIS 6.20 协议驱动程序。

NDIS 6.20 保留与早期 NDIS 版本的向后兼容性。 有关向后兼容性的详细信息，请参阅[NDIS 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。

若要更新协议驱动程序来支持 NDIS 6.20 环境，必须按如下所示修改 NDIS 6.x 协议驱动程序：

<a href="" id="build-environment-------"></a>**构建环境**   
替换 NDIS620 NDIS61 或 NDIS60 的预处理器定义。

<a href="" id="general-porting-requirements-------"></a>**移植的一般要求**   
-   使用 NDIS 6.20 版本替换已过时的接口。 有关已过时的接口的详细信息，请参阅[NDIS 6.20 中已过时接口](obsolete-interfaces-in-ndis-6-20.md)。

-   更新了以下接口来支持超过 64 个处理器：

    -   接收方缩放 (RSS)
    -   处理器信息设备驱动程序接口
    -   资源分配
    -   读取和写入锁

    支持超过 64 个处理器的详细信息，请参阅[支持多个 64 位处理器中 NDIS 6.20](support-for-more-than-64-processors-in-ndis-6-20.md)。

<a href="" id="driver-initialization-------"></a>**驱动程序初始化**   
-   将 NDIS 版本设置为在 6.20 **MajorNdisVersion**并**MinorNdisVersion**的成员[ **NDIS\_协议\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566825)结构，它传递给[ **NdisRegisterProtocolDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff564520)函数。

-   在中设置协议驱动程序版本**MajorDriverVersion**并**MinorDriverVersion** NDIS 成员\_协议\_驱动程序\_特征为适当的驱动程序特定值的结构。

<a href="" id="protocol-bind-and-unbind-operations-------"></a>**协议绑定和取消绑定操作**   
-   使用最新版本的微型端口适配器功能播发接口。 以下接口已经更新功能：
    -   电源管理
    -   电源管理
    -   接收方缩放 (RSS)
    -   硬件协助 (VMQ)
-   使用这些结构的更新的版本：

    -   [**NDIS\_BIND\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff564832)
    -   [**NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706)

    NDIS 结构版本信息有关的信息，请参阅[指定 NDIS 版本信息](specifying-ndis-version-information.md)。

<a href="" id="send-and-receive-data-paths-------"></a>**发送和接收数据路径**   
-   使用的更新的版本[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。

-   选择性地支持虚拟机队列 (VMQ) 接口。 有关 VMQ 的详细信息，请参阅[虚拟机队列 (VMQ) 在 NDIS 6.20](virtual-machine-queue--vmq--in-ndis-6-20.md)。

 

 





