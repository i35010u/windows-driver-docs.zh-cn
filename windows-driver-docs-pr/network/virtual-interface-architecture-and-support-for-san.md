---
title: 虚拟接口体系结构和 SAN 支持
description: 虚拟接口体系结构和 SAN 支持
ms.assetid: 83d28f33-7354-4f59-8b01-4842286f12fb
keywords:
- 系统区域网络 WDK、 VI 体系结构
- SAN WDK、 VI 体系结构
- VI 体系结构 WDK San
- 虚拟接口体系结构 WDK San
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6448456a819ba9501651ad91bdcde40e85d7e01
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577033"
---
# <a name="virtual-interface-architecture-and-support-for-san"></a>虚拟接口体系结构和 SAN 支持





虚拟接口 (VI) 体系结构，建议的 Compaq、 Intel 和 Microsoft，是 SAN NIC 和主机计算机系统之间的接口的设计。 此体系结构表示系统区域网络 (SAN) 方面的设计仅一个的方面。 有共享相同的基本特征的备选设计。

VI 体系结构定义的功能和特征的一组互连 SAN 设备。 例如，VI 体系结构包括支持远程直接内存访问 (RDMA) 操作。 VI 体系结构还介绍了与 SAN NIC 管理终结点和连接，并处理数据传输请求进行交互的特定机制。

Windows 套接字开关适用于广泛的一类 SAN 互连之外使用 VI 体系结构。 Windows 套接字的 SAN 扩展为特定的 SAN nic。 以下服务提供程序接口 (SPI) 防护罩将开关由硬件接口 该硬件接口封装在 SAN 服务提供程序 DLL 和其内核模式代理驱动程序。 由 SAN 供应商提供，这些组件。 SAN 扩展的详细信息，请参阅[Windows 套接字的 SPI 扩展 San](windows-sockets-spi-extensions-for-sans.md)。

 

 





