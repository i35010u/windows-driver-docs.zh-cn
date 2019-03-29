---
title: 管理虚拟功能
description: 管理虚拟功能
ms.assetid: 6B08B04D-C9A1-4159-9866-D179012191B2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31e39ae46525a657d36145ab137d2f78645c7975
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565973"
---
# <a name="managing-virtual-functions"></a>管理虚拟功能


本部分介绍支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器上的要求和管理 PCI Express (PCIe) 的虚函数 (VFs) 的指南。

本部分包括以下主题：

[虚函数初始化和拆卸概述](overview-of-virtual-function-initialization-and-teardown.md)

[为虚拟函数分配的资源](allocating-resources-for-a-virtual-function.md)

[对于虚拟函数释放资源](freeing-resources-for-a-virtual-function.md)

[枚举网络适配器上的虚函数](enumerating-virtual-functions-on-a-network-adapter.md)

[查询虚拟函数的参数](querying-the-parameters-of-a-virtual-function.md)

[访问 PCI 配置空间的虚拟函数](accessing-the-pci-configuration-space-of-a-virtual-function.md)

[设置虚拟函数的电源状态](setting-the-power-state-of-a-virtual-function.md)

[重置虚拟函数](resetting-a-virtual-function.md)

SR-IOV 网络适配器 VFs 的更多信息，请参阅[SR-IOV 虚拟功能 (VFs)](sr-iov-virtual-functions--vfs-.md)。

**请注意**  仅 PF 微型端口驱动程序可以配置网络适配器的硬件资源，例如 VFs。 VF 微型端口驱动程序不能直接访问的大多数 SR-IOV 适配器的硬件资源。 有关详细信息，请参阅[编写的 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





