---
title: 虚拟接口体系结构和 SAN 支持
description: 虚拟接口体系结构和 SAN 支持
keywords:
- 系统区域网络 WDK，VI 体系结构
- SAN WDK，VI 体系结构
- VI 体系结构 WDK San
- 虚拟接口体系结构 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8abf5731f159c837e71ed2b13d79c202a5b65d74
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802257"
---
# <a name="virtual-interface-architecture-and-support-for-san"></a>虚拟接口体系结构和 SAN 支持





虚拟接口 (由 Compaq、Intel 和 Microsoft 推荐的 VI) 体系结构，是 SAN NIC 与主计算机系统之间的接口设计。 此体系结构只代表了一种与系统区域网络 (SAN) 相关的设计方面。 有一些其他设计共享相同的基本特征。

VI 体系结构为 SAN 互连定义一组功能和特性。 例如，VI 体系结构支持 (RDMA) 操作的远程直接内存访问。 VI 体系结构还介绍了与 SAN NIC 交互以管理终结点和连接以及处理数据传输请求的特定机制。

Windows 套接字交换机与使用 VI 体系结构的更广泛的 SAN 互连类配合使用。  (SPI) 为 Windows 套接字服务提供程序接口提供的 SAN 扩展屏蔽了特定 SAN NIC 的硬件接口中的开关。 该硬件接口封装在 SAN 服务提供程序 DLL 及其内核模式代理驱动程序中。 这些组件由 SAN 供应商提供。 有关 SAN 扩展的详细信息，请参阅 [适用于 san 的 Windows 套接 SPI 扩展](windows-sockets-spi-extensions-for-sans.md)。

 

 





