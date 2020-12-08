---
title: 管理 NIC 交换机
description: 管理 NIC 交换机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b23b8fdebf48552ffbae1fa27c78c7c472f9268
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825073"
---
# <a name="managing-nic-switches"></a>管理 NIC 交换机


本部分介绍管理网络适配器的 NIC 交换机的要求和指导原则，该网络适配器支持单个根 i/o 虚拟化 (SR-IOV) 。 用于在 SR-IOV 网络适配器上管理 NIC 交换机的 PCI Express (PCIe) 物理功能 () PF 的微型端口驱动程序管理适配器上的 NIC 交换机。

本节包括下列主题：

[创建 NIC 交换机](creating-a-nic-switch.md)

[删除 NIC 交换机](deleting-a-nic-switch.md)

[枚举网络适配器上的 NIC 交换机](enumerating-nic-switches-on-a-network-adapter.md)

[查询 NIC 交换机的参数](querying-the-parameters-of-a-nic-switch.md)

[设置 NIC 交换机的参数](setting-the-parameters-of-a-nic-switch.md)

有关 SR-IOV 网络适配器的 NIC 交换机的详细信息，请参阅 [Nic 交换机](nic-switches.md)。

**注意**  只有 PF 微型端口驱动程序可以配置网络适配器的硬件资源，如 NIC 交换机。 用于 PCIe 虚拟功能 (VF) 在 SR-IOV 网络适配器上的微型端口驱动程序无法直接访问大多数适配器的硬件资源。 有关详细信息，请参阅 [编写 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





