---
title: 管理虚拟端口
description: 管理虚拟端口
ms.assetid: BF3DFE01-6583-4FBB-AFFA-2C017A3D9A05
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 806f9af053dee9448fbfed201a2e83551f9dab1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521861"
---
# <a name="managing-virtual-ports"></a>管理虚拟端口


本部分介绍的要求和管理在 NIC 的交换机上的虚拟端口 (VPorts) 的指南。 此交换机提供的支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器。

本部分包括以下主题：

[创建虚拟端口](creating-a-virtual-port.md)

[正在删除虚拟端口](deleting-a-virtual-port.md)

[枚举网络适配器上的虚拟端口](enumerating-virtual-ports-on-a-network-adapter.md)

[查询的参数的虚拟端口](querying-the-parameters-of-a-virtual-port.md)

[设置虚拟端口的参数](setting-the-parameters-of-a-virtual-port.md)

[管理虚拟端口的接收筛选器](managing-receive-filters-for-a-virtual-port.md)

[队列对的对称和非对称分配](symmetric-and-asymmetric-assignment-of-queue-pairs.md)

[通过虚拟端口的数据包流](packet-flow-over-a-virtual-port.md)

[非默认的虚拟端口和 VMQ](nondefault-virtual-ports-and-vmq.md)

VPorts 的详细信息，请参阅[虚拟端口 (VPorts)](virtual-ports--vports-.md)。

有关 NIC 开关的详细信息，请参阅[NIC 开关](nic-switches.md)。

**请注意**  仅微型端口驱动程序为 PCI Express (PCIe) 物理函数 (PF) 可以配置网络适配器的硬件资源，例如 VPorts。 微型端口驱动程序 PCIe 虚拟函数 (VF) 为不能直接访问的大多数 SR-IOV 适配器的硬件资源。 有关详细信息，请参阅[编写的 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





