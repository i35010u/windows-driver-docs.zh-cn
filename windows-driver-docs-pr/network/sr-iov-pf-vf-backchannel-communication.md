---
title: SR-IOV PF/VF 反向通道通信概述
description: SR-IOV PF/VF 反向通道通信概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8b1915a4d2fb4ac66827f7de0b3ef574219ce29
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834319"
---
# <a name="sr-iov-pfvf-backchannel-communication-overview"></a>SR-IOV PF/VF 反向通道通信概述


单个根 i/o 虚拟化 (SR-IOV) 接口在 PCI Express (PCIe 的微型端口驱动程序之间提供通信通道（或 *backchannel*），) 虚函数 (VF) 和 PCIe 物理功能 (PF) 。 每个 VF 微型端口驱动程序都可以通过 backchannel 将请求发送到 PF 微型端口驱动程序。 PF 小型端口驱动程序可以通过 backchannel 将状态通知发送到单个 VF 微型端口驱动程序。

通过 backchannel 接口在 PF 和 VF 微型端口驱动程序之间交换的数据涉及使用 *VF 配置块*。 每个 VF 配置块在概念上类似于进程间通信 (IPC) 消息，其中每个块都有一个专用的格式、长度和块标识符。 独立硬件供应商 (IHV) 可以为 PF 和 VF 微型端口驱动程序定义一个或多个 VF 配置块。

本节包括下列主题：

[从 VF 微型端口驱动程序进行反向通道通信](backchannel-communication-from-a-vf-miniport-driver.md)

[从 PF 微型端口驱动程序进行反向通道通信](backchannel-communication-from-the-pf-miniport-driver.md)

 

 





