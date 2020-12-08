---
title: 有关初始化和解除虚拟功能的概述
description: 有关初始化和解除虚拟功能的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35bb3ca9144dc0c0c997c2e188477dec301543c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815919"
---
# <a name="overview-of-virtual-function-initialization-and-teardown"></a>有关初始化和解除虚拟功能的概述


本部分概述了 PCI Express (PCIe) 虚功能 (VFs) 的初始化和拆卸序列。 VFs 由支持单个根 i/o 虚拟化 (SR-IOV) 的网络适配器提供。

本节包括下列主题：

[虚拟功能初始化序列](virtual-function-initialization-sequence.md)

[虚拟功能解除序列](virtual-function-teardown-sequence.md)

有关适用于 SR-IOV 网络适配器的 VFs 的详细信息，请参阅 [Sr-iov 虚拟功能 (VFs) ](sr-iov-virtual-functions--vfs-.md)。

**注意**  只有 PF 微型端口驱动程序可以配置网络适配器的硬件资源，如 VFs。 VF 微型端口驱动程序无法直接访问大多数 SR-IOV 适配器的硬件资源。 有关详细信息，请参阅 [编写 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





