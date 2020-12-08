---
title: 管理虚拟端口
description: 管理虚拟端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d6db5cf8b89d441a4ad5bec5bf7b3cc825e21c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833377"
---
# <a name="managing-virtual-ports"></a>管理虚拟端口


本部分介绍管理 NIC 交换机上 (VPorts) 的虚拟端口的要求和指导原则。 此开关由支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器提供。

本节包括下列主题：

[创建虚拟端口](creating-a-virtual-port.md)

[删除虚拟端口](deleting-a-virtual-port.md)

[枚举网络适配器上的虚拟端口](enumerating-virtual-ports-on-a-network-adapter.md)

[查询虚拟端口的参数](querying-the-parameters-of-a-virtual-port.md)

[设置虚拟端口的参数](setting-the-parameters-of-a-virtual-port.md)

[管理虚拟端口的接收筛选器](managing-receive-filters-for-a-virtual-port.md)

[队列对的对称和非对称分配](symmetric-and-asymmetric-assignment-of-queue-pairs.md)

[基于虚拟端口的数据包流](packet-flow-over-a-virtual-port.md)

[非默认虚拟端口和 VMQ](nondefault-virtual-ports-and-vmq.md)

有关 VPorts 的详细信息，请参阅 [虚拟端口 (VPorts) ](virtual-ports--vports-.md)。

有关 NIC 交换机的详细信息，请参阅 [Nic 交换机](nic-switches.md)。

**注意**  只有 PCI Express (PCIe 的微型端口驱动程序) 物理功能 (PF) 可以配置网络适配器的硬件资源，如 VPorts。 PCIe 虚拟功能 (VF) 的微型端口驱动程序无法直接访问大多数 SR-IOV 适配器的硬件资源。 有关详细信息，请参阅 [编写 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





