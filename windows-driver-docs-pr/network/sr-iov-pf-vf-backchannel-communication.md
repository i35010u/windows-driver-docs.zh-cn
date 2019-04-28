---
title: SR-IOV PF/VF 反向通道通信
description: SR-IOV PF/VF 反向通道通信
ms.assetid: 66D40452-1286-449E-BD6B-AFAD466E03A1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1416a113c4563a2c54963b5fc4930d9175cc88c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346037"
---
# <a name="sr-iov-pfvf-backchannel-communication"></a>SR-IOV PF/VF 反向通道通信


单根 I/O 虚拟化 (SR-IOV) 接口提供通信通道，或*backchannel*，PCI Express (PCIe) 虚拟函数 (VF) 和 PCIe 物理函数 (PF) 的微型端口驱动程序之间。 每个 VF 微型端口驱动程序可以通过反向通道向 PF 微型端口驱动程序发出请求。 PF 微型端口驱动程序可以向单个 VF 微型端口驱动程序通过反向通道发出状态通知。

对 backchannel 界面 PF 和 VF 微型端口驱动程序之间交换数据涉及到使用*VF 配置块*。 每个 VF 配置块是在概念上类似于进程间通信 (IPC) 消息，其中每个块都有一种专有格式，长度，并阻止标识符。 独立硬件供应商 (IHV) 可以定义一个或多个 VF 配置块 PF 和 VF 微型端口驱动程序。

本部分包括以下主题：

[Backchannel 通信从 VF 微型端口驱动程序](backchannel-communication-from-a-vf-miniport-driver.md)

[PF 微型端口驱动程序从 Backchannel 通信](backchannel-communication-from-the-pf-miniport-driver.md)

 

 





