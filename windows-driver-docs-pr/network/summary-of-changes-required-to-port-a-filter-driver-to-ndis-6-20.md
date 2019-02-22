---
title: 若要移植到 NDIS 6.20 的筛选器驱动程序所需的更改的摘要
description: 若要移植到 NDIS 6.20 的筛选器驱动程序所需的更改的摘要
ms.assetid: faf83399-b9ac-41b3-a891-0142ded422b3
keywords:
- NDIS 6.20 WDK，将筛选器驱动程序移植
- 移植到 NDIS 6.20 WDK 的筛选器驱动程序
- 筛选器驱动程序 WDK
- 筛选器驱动程序 WDK，移植到 NDIS 6.20
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 333da3504df95acc12816b8e0b16396dd1bfe345
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541402"
---
# <a name="summary-of-changes-required-to-port-a-filter-driver-to-ndis-620"></a>若要移植到 NDIS 6.20 的筛选器驱动程序所需的更改的摘要





本主题概述了所需端口 NDIS 6 的更改。*x*到 NDIS 6.20 的筛选器驱动程序。

NDIS 6.20 保留与早期 NDIS 版本的向后兼容性。 有关向后兼容性的详细信息，请参阅[NDIS 6.20 向后兼容性](ndis-6-20-backward-compatibility.md)。

若要更新筛选器驱动程序来支持 NDIS 6.20 环境，必须按如下所示修改 NDIS 6.x 筛选器驱动程序：

<a href="" id="build-environment"></a>**构建环境**  
替换 NDIS620 NDIS61 或 NDIS60 的预处理器定义。

<a href="" id="general-porting-requirements"></a>**移植的一般要求**  
-   使用 NDIS 6.20 版本替换已过时的接口。 有关已过时的接口的详细信息，请参阅[NDIS 6.20 中已过时接口](obsolete-interfaces-in-ndis-6-20.md)。

-   更新了以下接口来支持超过 64 个处理器：

    -   接收方缩放 (RSS)
    -   处理器信息设备驱动程序接口
    -   资源分配
    -   读取和写入锁

    支持超过 64 个处理器的详细信息，请参阅[支持多个 64 位处理器中 NDIS 6.20](support-for-more-than-64-processors-in-ndis-6-20.md)。

<a href="" id="driver-initialization"></a>**驱动程序初始化**  
-   将 NDIS 版本设置为在 6.20 **MajorNdisVersion**并**MinorNdisVersion**的成员[ **NDIS\_筛选器\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565515)结构，它传递给[ **NdisFRegisterFilterDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff562608)函数。

-   在中设置筛选器驱动程序版本**MajorDriverVersion**并**MinorDriverVersion** NDIS 成员\_筛选器\_驱动程序\_特征结构为适当的驱动程序特定值。

<a href="" id="filter-module-attach-and-detach-operations"></a>**筛选器模块中附加和分离操作**  
-   使用最新版本的微型端口适配器功能播发接口。 以下接口已经更新功能：
    -   电源管理
    -   接收方缩放 (RSS)
    -   硬件协助 (VMQ)
-   使用这些结构的更新的版本：

    -   [**NDIS\_FILTER\_ATTACH\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff565481)
    -   [**NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706)

    NDIS 结构版本信息有关的信息，请参阅[指定 NDIS 版本信息](specifying-ndis-version-information.md)。

<a href="" id="send-and-receive-data-paths"></a>**发送和接收数据路径**  
-   使用的更新的版本[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)结构。

-   选择性地支持虚拟机队列 (VMQ) 接口。 有关 VMQ 的详细信息，请参阅[虚拟机队列 (VMQ) 在 NDIS 6.20](virtual-machine-queue--vmq--in-ndis-6-20.md)。

 

 





