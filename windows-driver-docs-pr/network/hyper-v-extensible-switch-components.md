---
title: Hyper-v 可扩展交换机组件概述
description: Hyper-v 可扩展交换机组件概述
ms.assetid: 510A4D75-8DB4-46D7-BA54-248ED4FEC349
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4aa27402d33432b827e7861c8e36e7d0979aa4a
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565763"
---
# <a name="hyper-v-extensible-switch-components-overview"></a>Hyper-v 可扩展交换机组件概述


从 Windows Server 2012 开始, Hyper-v 可扩展交换机支持一个接口, 该接口允许 NDIS 筛选器驱动程序 (称为*hyper-v 可扩展交换机扩展*) 在可扩展交换机驱动程序堆栈中进行绑定。 这样, 扩展可以监视、修改数据包并将数据包转发到可扩展的交换机端口。 这还允许扩展插件将数据包丢弃、重定向或发起到 Hyper-v 分区使用的端口。

可以使用策略来预配扩展, 这些策略适用于单个可扩展交换机端口或交换机本身的数据包通信。 这允许该扩展允许发送或拒绝数据包的发送。

下图显示了 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的可扩展交换机接口的组件。

![说明 ndis 6.40\-和更高版本的 hyper-v 可扩展交换机体系结构的示意图](images/vswitcharchitecture-ndis640.png)

下图显示了用于 NDIS 6.30 的可扩展交换机接口 (Windows Server 2012) 的组件。

![用 sr-iov 说明综合设备数据路径的示意图](images/vswitcharchitecture.png)

本部分包含以下主题, 其中介绍了可扩展交换机组件:

[Hyper-v 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)

[Hyper-v 可扩展交换机端口](hyper-v-extensible-switch-ports.md)

[Hyper-v 可扩展交换机网络适配器](hyper-v-extensible-switch-network-adapters.md)

[Hyper-v 可扩展交换机端口和网络适配器状态](hyper-v-extensible-switch-port-and-network-adapter-states.md)

 

 





