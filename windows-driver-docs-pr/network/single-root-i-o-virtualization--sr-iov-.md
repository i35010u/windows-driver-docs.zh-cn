---
title: 单根 I/O 虚拟化 (SR-IOV) 简介
description: 单根 I/O 虚拟化 (SR-IOV) 简介
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0263838101366c27f4b81bbd4f2f57af67f57c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836287"
---
# <a name="introduction-to-single-root-io-virtualization-sr-iov"></a>单根 I/O 虚拟化 (SR-IOV) 简介


本部分介绍 NDIS 单根 i/o 虚拟化 (SR-IOV) 接口。 从 NDIS 6.30 开始，SR-IOV 接口为 Windows Server 2012 和更高版本的 Windows Server 上的虚拟化网络支持 Microsoft Hyper-V 性能改进。

来自 PCI-SIG 的 SR-IOV 规范定义 PCI Express (PCIe) 规范套件的扩展，使多个虚拟机 (Vm) 共享同一 PCIe 物理硬件资源。 本部分描述了 NDIS SR-IOV 接口，并介绍了为实现 PCIe SR-IOV 规范的支持 SR-IOV 的网络适配器编写 NDIS 微型端口驱动程序的方法。

本节包括下列主题：

[单根 I/O 虚拟化 (SR-IOV) 概述](overview-of-single-root-i-o-virtualization--sr-iov-.md)

[编写 SR-IOV PF 微型端口驱动程序](writing-sr-iov-pf-miniport-drivers.md)

[编写 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)

[SR-IOV PF/VF 反向通道通信](sr-iov-pf-vf-backchannel-communication.md)

[SR-IOV OID](sr-iov-oids.md)

有关 SR-IOV 的详细信息，请参阅 PCI-SIG [单根 I/o 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742) 规范。

 

 





