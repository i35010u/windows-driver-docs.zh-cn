---
title: 捕获扩展
description: 捕获扩展
ms.assetid: A8C2E550-4B1F-4DDB-B97F-1F7B6B74F5E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad4bbbe87b0415e99822f138954ed8813001b85e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213991"
---
# <a name="capturing-extensions"></a>捕获扩展


Hyper-v 可扩展交换机捕获扩展检查数据包流量、对象标识符 (OID) 请求，以及 NDIS 状态指示。 这种类型的扩展不能修改或丢弃数据包，也不能排除数据包被传递到可扩展交换机端口。 但是，捕获扩展可能会产生数据包流量，例如包含扩展发送到主机应用程序的流量统计信息的数据包。

捕获扩展是在入口数据路径开头和传出数据路径结束时调用的。 有关这些数据路径的详细信息，请参阅 [Hyper-v 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

捕获扩展具有以下要求和限制：

-   捕获扩展必须开发为支持可扩展交换机接口的 NDIS 筛选器驱动程序。

    有关筛选器驱动程序的详细信息，请参阅 [NDIS 筛选器驱动程序](./roadmap-for-developing-ndis-filter-drivers.md)。

    有关如何编写捕获扩展的详细信息，请参阅 [编写 Hyper-v 可扩展交换机扩展](writing-hyper-v-extensible-switch-extensions.md)。

-   捕获扩展提供了与标准 NDIS 监视筛选器驱动程序相同的功能。 但是，捕获扩展的 INF 文件必须将其安装为修改筛选器驱动程序。

    有关修改筛选器驱动程序的详细信息，请参阅 [筛选器驱动程序的类型](types-of-filter-drivers.md)。

    有关修改筛选器驱动程序的 INF 要求的详细信息，请参阅 [配置修改筛选器驱动程序的 Inf 文件](configuring-an-inf-file-for-a-modifying-filter-driver.md)。

-   捕获扩展可通过入口和出口的可扩展交换机数据路径来监视数据包。 但是，这种类型的扩展必须始终调用 [**NdisFSendNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsendnetbufferlists) ，将数据包转发到可扩展交换机驱动程序堆栈中的底层驱动程序，而不是完成它们。

-   捕获扩展不能修改数据包中的数据，也不能将端口目标添加到带外 (OOB) 数据包数据。 扩展不能将数据包传递到任何可扩展交换机端口。

-   捕获扩展可产生数据包。 例如，扩展可能会产生数据包，以便向远程监视应用程序报告流量状态。

    若要详细了解如何通过扩展来发起数据包，请参阅 [原始数据包流量](originating-packet-traffic.md)。

    **注意**   与其他扩展一样，捕获扩展只能在可扩展交换机入口数据路径中产生数据包流量。

     

-   捕获扩展可以监视通过可扩展交换机驱动程序堆栈发出的数据包、OID 请求和 NDIS 状态指示。 但是，这种类型的扩展必须通过可扩展交换机驱动程序堆栈转发数据包、OID 请求和 NDIS 状态指示。 扩展不得修改它所监视的数据包、OID 请求或 NDIS 状态指示内的数据。

-   必须将扩展 INF 文件中的 **FilterClass** 值设置为 **ms \_ 交换机 \_ 捕获**。 有关详细信息，请参阅 [Hyper-v 可扩展交换机扩展的 INF 要求](inf-requirements-for-hyper-v-extensions.md)。

-   可以将任意数量的捕获扩展绑定到可扩展的交换机实例。 默认情况下，多个捕获扩展基于其安装时间进行排序。 例如，多个捕获扩展在可扩展交换机驱动程序堆栈中分层，其中最新安装的扩展位于堆栈中的其他捕获扩展之上。

    绑定到可扩展交换机实例后，可对可扩展交换机驱动程序堆栈中捕获扩展的分层进行重新排序。 有关详细信息，请参阅对 [Hyper-v 可扩展交换机扩展重新排序](reordering-hyper-v-extensibility-switch-extensions.md)。

 

