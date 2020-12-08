---
title: 访问虚拟功能的 PCI 配置空间
description: 访问虚拟功能的 PCI 配置空间
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ed084e9bbea74246b19c72890823bbb9444dae8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825553"
---
# <a name="accessing-the-pci-configuration-space-of-a-virtual-function"></a>访问虚拟功能的 PCI 配置空间


本部分介绍了从 PCI Express (PCIe) 虚功能 (VFs) 的 PCI 配置空间访问数据的指南。 VFs 是网络适配器的硬件功能，它支持 (SR-IOV) 的单个根 i/o 虚拟化。

本节包括下列主题：

[查询虚拟功能的 PCI 配置数据](overview-of-virtual-function-initialization-and-teardown.md)

[设置虚拟功能的 PCI 配置数据](allocating-resources-for-a-virtual-function.md)

有关适用于 SR-IOV 网络适配器的 VFs 的详细信息，请参阅 [Sr-iov 虚拟功能 (VFs) ](sr-iov-virtual-functions--vfs-.md)。

**注意**  只有 PF 微型端口驱动程序可以为 VF 配置 PCI 配置空间。 VF 微型端口驱动程序无法直接访问大多数 SR-IOV 适配器的硬件资源，如 PCI 配置空间。 有关详细信息，请参阅 [编写 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





