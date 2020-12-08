---
title: 虚拟机队列 (VMQ) 概述
description: 虚拟机队列 (VMQ) 概述
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4c304360803533f27dbb8cfc38109f8abab4a6fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802235"
---
# <a name="virtual-machine-queue-vmq-overview"></a>虚拟机队列 (VMQ) 概述

在 Windows Server 2008 R2 和更高版本的 Windows server 中，NDIS 虚拟机队列 (VMQ) 接口支持 Microsoft Hyper-V 网络性能6.20 改进。

- [虚拟机队列体系结构](virtual-machine-queue-architecture.md) 介绍了 VMQ 体系结构的高级概念。

- [写入 VMQ 驱动程序](writing-vmq-drivers.md) 提供有关编写 NDIS VMQ 驱动程序的更多详细信息。

> [!NOTE]
> 务必研究 [NDIS 虚拟微端口驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/network/ndis/netvmini/6x)，尤其是 vmq 和 vmq 源文件。

VMQ 接口支持：

- 通过使用目标 media access control (MAC) 地址来分类网络适配器硬件中接收的数据包，以将数据包路由到不同的接收队列。

- 共享内存;有关详细信息，请参阅 [NDIS 内存管理接口](/windows-hardware/drivers/ddi/_netvista/)。

- 通过处理不同处理器上不同虚拟机的数据包，缩放到多个处理器。

## <a name="related-topics"></a>相关主题

- [虚拟机队列体系结构](virtual-machine-queue-architecture.md)
- [编写 VMQ 驱动程序](writing-vmq-drivers.md)
