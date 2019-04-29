---
title: 有关初始化和解除虚拟功能的概述
description: 有关初始化和解除虚拟功能的概述
ms.assetid: 2684A93A-40C2-49DA-925D-2BAACA9F8CD9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e820d0fc55766f0bf410c49d9e858dc9f7555690
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372890"
---
# <a name="overview-of-virtual-function-initialization-and-teardown"></a>有关初始化和解除虚拟功能的概述


本部分概述了对 PCI Express (PCIe) 虚函数 (VFs) 的初始化和拆卸序列。 VFs 提供了支持单个根 I/O 虚拟化 (SR-IOV) 的网络适配器。

本部分包括以下主题：

[虚函数初始化序列](virtual-function-initialization-sequence.md)

[虚函数拆卸序列](virtual-function-teardown-sequence.md)

SR-IOV 网络适配器 VFs 的更多信息，请参阅[SR-IOV 虚拟功能 (VFs)](sr-iov-virtual-functions--vfs-.md)。

**请注意**  仅 PF 微型端口驱动程序可以配置网络适配器的硬件资源，例如 VFs。 VF 微型端口驱动程序不能直接访问的大多数 SR-IOV 适配器的硬件资源。 有关详细信息，请参阅[编写的 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)。

 

 

 





