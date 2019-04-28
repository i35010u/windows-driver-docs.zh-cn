---
title: 单根 I/O 虚拟化 (SR-IOV)
description: 单根 I/O 虚拟化 (SR-IOV)
ms.assetid: E64DD4F0-D5F8-4FFF-931B-C04C5C42D000
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b1b288c0c8852a9b54089f269957512fe043f24
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342280"
---
# <a name="single-root-io-virtualization-sr-iov"></a>单根 I/O 虚拟化 (SR-IOV)


本部分介绍 NDIS 单根 I/O 虚拟化 (SR-IOV) 接口。 从开始 NDIS 6.30，SR-IOV 接口支持 Microsoft HYPER-V 的性能改进 Windows Server 2012 和更高版本的 Windows Server 上的虚拟化网络。

从 PCI SIG SR-IOV 规范定义扩展到 PCI Express (PCIe) 规范 suite 使多个虚拟机 (Vm) 共享同一 PCIe 物理硬件资源。 本部分介绍的 NDIS SR-IOV 接口，并介绍用于编写实现 PCIe SR-IOV 规范为 SR-IOV 功能的网络适配器的 NDIS 微型端口驱动程序的技术。

本部分包括以下主题：

[单根 I/O 虚拟化 (SR-IOV) 的概述](overview-of-single-root-i-o-virtualization--sr-iov-.md)

[编写的 SR-IOV PF 微型端口驱动程序](writing-sr-iov-pf-miniport-drivers.md)

[编写的 SR-IOV VF 微型端口驱动程序](writing-sr-iov-vf-miniport-drivers.md)

[SR-IOV PF/取景器 Backchannel 通信](sr-iov-pf-vf-backchannel-communication.md)

[SR-IOV 的 Oid](sr-iov-oids.md)

有关 SR-IOV 的详细信息，请参阅 PCI SIG[单根 I/O 虚拟化和共享 1.1](https://go.microsoft.com/fwlink/p/?linkid=221742)规范。

 

 





