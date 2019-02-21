---
title: HYPER-V 可扩展交换机组件
description: HYPER-V 可扩展交换机组件
ms.assetid: 510A4D75-8DB4-46D7-BA54-248ED4FEC349
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cff31c4e67ebb02218729c2cc1afa4914bce076
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555292"
---
# <a name="hyper-v-extensible-switch-components"></a>HYPER-V 可扩展交换机组件


从 Windows Server 2012 开始，HYPER-V 可扩展交换机支持允许 NDIS 筛选器驱动程序的接口 (称为*HYPER-V 可扩展交换机扩展*) 要在可扩展交换机驱动程序堆栈中绑定。 这允许扩展监视、 修改和将数据包转发到可扩展的交换机端口。 这也允许扩展来删除、 重定向，或源自 HYPER-V 分区都使用的端口的数据包。

扩展可以使用可通过单个可扩展的交换机端口或交换机自身应用到数据包流量的策略设置。 这样，要允许或拒绝来自正在发送的数据包将发送数据包的扩展。

下图显示了可扩展交换机接口 NDIS 6.40 (Windows Server 2012 R2) 和更高版本的组件。

![关系图阐释超\-ndis 6.40 及更高版本的 v 可扩展交换机体系结构](images/vswitcharchitecture-ndis640.png)

下图显示了可扩展交换机接口的组件的 NDIS 6.30 (Windows Server 2012)。

![说明与 sr-iov 的合成设备数据路径的关系图](images/vswitcharchitecture.png)

本部分包括描述可扩展交换机组件的以下主题：

[HYPER-V 可扩展交换机扩展](hyper-v-extensible-switch-extensions.md)

[HYPER-V 可扩展交换机端口](hyper-v-extensible-switch-ports.md)

[HYPER-V 可扩展交换机的网络适配器](hyper-v-extensible-switch-network-adapters.md)

[HYPER-V 可扩展交换机端口和网络适配器状态](hyper-v-extensible-switch-port-and-network-adapter-states.md)

 

 





