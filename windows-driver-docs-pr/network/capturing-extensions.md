---
title: 捕获扩展
description: 捕获扩展
ms.assetid: A8C2E550-4B1F-4DDB-B97F-1F7B6B74F5E7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d260e5edb69b902c3b4c84539ca34408bb24bc3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351944"
---
# <a name="capturing-extensions"></a>捕获扩展


捕获扩展的 HYPER-V 可扩展交换机检查数据包流量、 对象标识符 (OID) 请求和 NDIS 状态指示。 此类型的扩展不能修改或丢弃的数据包，或从正被传递到可扩展的交换机端口中排除的数据包。 但是，捕获扩展可以源自数据包流量，例如包，其中包含扩展将发送到主机应用程序的流量统计数据。

捕获扩展调用的入口数据路径的开头和末尾的出口数据路径。 有关这些数据路径的详细信息，请参阅[HYPER-V 可扩展交换机数据路径](hyper-v-extensible-switch-data-path.md)。

捕获扩展具有以下要求和限制：

-   捕获扩展必须作为支持可扩展交换机接口的 NDIS 筛选器驱动程序开发。

    有关筛选器驱动程序的详细信息，请参阅[NDIS 筛选器驱动程序](ndis-filter-drivers2.md)。

    有关如何编写捕获扩展的详细信息，请参阅[编写的 HYPER-V 可扩展交换机扩展](writing-hyper-v-extensible-switch-extensions.md)。

-   捕获扩展提供了与标准 NDIS 监视筛选器驱动程序相同的功能。 但是，捕获扩展的 INF 文件必须安装它为修改的筛选器驱动程序。

    有关修改筛选器驱动程序的详细信息，请参阅[类型的筛选器驱动程序](types-of-filter-drivers.md)。

    修改筛选器驱动程序的 INF 要求的详细信息，请参阅[配置修改筛选器驱动程序 INF 文件](configuring-an-inf-file-for-a-modifying-filter-driver.md)。

-   捕获扩展可以监视数据包通过入口和出口可扩展交换机数据路径。 但是，此类型的扩展必须始终调用[ **NdisFSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff562616)将数据包转发给可扩展交换机驱动程序堆栈中的基础驱动程序并不完成它们。

-   捕获扩展必须不修改这些包中的数据也不会将端口目标添加到该数据包的带外 (OOB) 数据。 扩展必须不免除任何可扩展交换机端口的数据包传送。

-   捕获扩展可以源自数据包。 例如，该扩展可能来源中对报表到远程监视应用程序的交通状况的顺序的数据包。

    由扩展原始数据包的详细信息，请参阅[源自数据包流量](originating-packet-traffic.md)。

    **请注意**  如与其他扩展，捕获扩展可以仅由可扩展交换机入口数据路径中的数据包流量。

     

-   捕获扩展可以监视数据包、 OID 请求和通过可扩展交换机驱动程序堆栈发出的 NDIS 状态指示。 但是，此类型的扩展必须转发数据包、 OID 请求和 NDIS 状态指示通过可扩展交换机驱动程序堆栈。 该扩展不能修改在数据包、 OID 请求或 NDIS 状态指示对其所监视的数据。

-   **FilterClass**值 INF 文件中的扩展必须设置为**ms\_切换\_捕获**。 有关详细信息，请参阅[INF 的 HYPER-V 可扩展交换机扩展的要求](inf-requirements-for-hyper-v-extensions.md)。

-   任意数量的捕获扩展可以绑定到可扩展交换机实例。 默认情况下，多个捕获扩展排序基于安装时。 例如，多个捕获扩展的分层在可扩展交换机驱动程序堆栈中使用最近安装的扩展在堆栈中的其他捕获扩展的上面。

    绑定到可扩展交换机实例后，可以重新捕获可扩展交换机驱动程序堆栈中的扩展的分层。 有关详细信息，请参阅[重新排序的 HYPER-V 可扩展交换机扩展](reordering-hyper-v-extensibility-switch-extensions.md)。

 

 





