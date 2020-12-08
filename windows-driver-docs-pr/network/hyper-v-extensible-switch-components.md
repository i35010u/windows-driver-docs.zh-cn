---
title: Hyper-V 可扩展交换机组件概述
description: Hyper-V 可扩展交换机组件概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfdfb7277f40f617774565c9d8aac204cd7d2639
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795461"
---
# <a name="hyper-v-extensible-switch-components-overview"></a>Hyper-V 可扩展交换机组件概述


从 Windows Server 2012 开始，Hyper-v 可扩展交换机支持一个接口，该接口允许 (称为 *hyper-v 可扩展交换机扩展*) 在可扩展交换机驱动程序堆栈内绑定的 NDIS 筛选器驱动程序。 这样，扩展可以监视、修改数据包并将数据包转发到可扩展的交换机端口。 这还允许扩展插件将数据包丢弃、重定向或发起到 Hyper-v 分区使用的端口。

可以使用策略来预配扩展，这些策略适用于单个可扩展交换机端口或交换机本身的数据包通信。 这允许该扩展允许发送或拒绝数据包的发送。

下图显示了 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的可扩展交换机接口的组件。

![说明 \- ndis 6.40 和更高版本的 hyper-v 可扩展交换机体系结构的示意图](images/vswitcharchitecture-ndis640.png)

下图显示了 NDIS 6.30 (Windows Server 2012) 的可扩展交换机接口组件。

![用 sr-iov 说明综合设备数据路径的示意图](images/vswitcharchitecture.png)

本部分包含以下主题，其中介绍了可扩展交换机组件：

[Hyper-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)

[Hyper-V 可扩展交换机端口](hyper-v-extensible-switch-ports.md)

[Hyper-V 可扩展交换机网络适配器](hyper-v-extensible-switch-network-adapters.md)

[Hyper-V 可扩展交换机端口和网络适配器状态](hyper-v-extensible-switch-port-and-network-adapter-states.md)

 

 





