---
title: 访问虚拟功能的 PCI 配置空间
description: 访问虚拟功能的 PCI 配置空间
ms.assetid: 727E6FC5-F61F-4CB0-B6EB-9B372F2C59E1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 529a8dcfd23614f9edf881302cb5209b6f9644ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367950"
---
# <a name="accessing-the-pci-configuration-space-of-a-virtual-function"></a>访问虚拟功能的 PCI 配置空间


本部分介绍从 PCI 配置空间 PCI Express (PCIe) 虚函数 (VFs) 的访问的数据的指导原则。 VFs 是支持单根 I/O 虚拟化 (SR-IOV) 的网络适配器的硬件功能。

本部分包括以下主题：

[查询虚函数的 PCI 配置的数据](overview-of-virtual-function-initialization-and-teardown.md)

[设置虚拟函数的 PCI 配置数据](allocating-resources-for-a-virtual-function.md)

SR-IOV 网络适配器 VFs 的更多信息，请参阅[SR-IOV 虚拟功能 (VFs)](sr-iov-virtual-functions--vfs-.md)。

**请注意**  仅 PF 微型端口驱动程序可以为 VF 配置 PCI 配置空间。 VF 微型端口驱动程序不能直接访问大部分 SR-IOV 适配器的硬件资源，如 PCI 配置空间。 有关详细信息，请参阅[编写的 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





