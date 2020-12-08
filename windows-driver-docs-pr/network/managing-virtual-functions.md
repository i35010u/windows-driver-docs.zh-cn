---
title: 管理虚拟功能
description: 管理虚拟功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c23683d8de64b45ce1d7ee1a7718c5268bd5213
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833381"
---
# <a name="managing-virtual-functions"></a>管理虚拟功能


本部分介绍在支持单一根 i/o 虚拟化 (SR-IOV) 的网络适配器上，如何管理 PCI Express (PCIe) 虚功能)  (的要求和指导原则。

本节包括下列主题：

[有关初始化和解除虚拟功能的概述](overview-of-virtual-function-initialization-and-teardown.md)

[为虚拟功能分配资源](allocating-resources-for-a-virtual-function.md)

[为虚拟功能释放资源](freeing-resources-for-a-virtual-function.md)

[枚举网络适配器上的虚拟功能](enumerating-virtual-functions-on-a-network-adapter.md)

[查询虚拟功能的参数](querying-the-parameters-of-a-virtual-function.md)

[访问虚拟功能的 PCI 配置空间](accessing-the-pci-configuration-space-of-a-virtual-function.md)

[设置虚拟功能的电源状态](setting-the-power-state-of-a-virtual-function.md)

[重置虚拟功能](resetting-a-virtual-function.md)

有关适用于 SR-IOV 网络适配器的 VFs 的详细信息，请参阅 [Sr-iov 虚拟功能 (VFs) ](sr-iov-virtual-functions--vfs-.md)。

**注意**  只有 PF 微型端口驱动程序可以配置网络适配器的硬件资源，如 VFs。 VF 微型端口驱动程序无法直接访问大多数 SR-IOV 适配器的硬件资源。 有关详细信息，请参阅 [编写 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





