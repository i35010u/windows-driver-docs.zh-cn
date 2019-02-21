---
title: 管理 NIC 开关
description: 管理 NIC 开关
ms.assetid: EE198C8D-427B-4013-8D19-5323332A4D87
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2972ccf8272335c115c40929722024b57eefaf62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542568"
---
# <a name="managing-nic-switches"></a>管理 NIC 开关


本部分介绍的要求和管理支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器上的 NIC 开关的指南。 有关 PCI Express (PCIe) 物理函数 (PF) 的 SR-IOV 网络适配器的微型端口驱动程序管理适配器上的 NIC 开关。

本部分包括以下主题：

[创建 NIC 交换机](creating-a-nic-switch.md)

[删除 NIC 开关](deleting-a-nic-switch.md)

[枚举的网络适配器上的 NIC 开关](enumerating-nic-switches-on-a-network-adapter.md)

[查询 NIC 开关的参数](querying-the-parameters-of-a-nic-switch.md)

[设置 NIC 开关的参数](setting-the-parameters-of-a-nic-switch.md)

SR-IOV 网络适配器的 NIC 开关的详细信息，请参阅[NIC 开关](nic-switches.md)。

**请注意**  仅 PF 微型端口驱动程序可以配置网络适配器的硬件资源，例如 NIC 开关。 微型端口驱动程序为 PCIe 虚拟函数 (VF) 的 SR-IOV 网络适配器上不能直接访问的大多数适配器的硬件资源。 有关详细信息，请参阅[编写的 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





