---
title: SR-IOV PF/VF Backchannel 通信概述
description: SR-IOV PF/VF Backchannel 通信概述
ms.assetid: 66D40452-1286-449E-BD6B-AFAD466E03A1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 973626fc5f4a19a39892412b1c0797bba06d5dd1
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565635"
---
# <a name="sr-iov-pfvf-backchannel-communication-overview"></a>SR-IOV PF/VF Backchannel 通信概述


单个根 i/o 虚拟化 (SR-IOV) 接口在 PCI Express (PCIe) 虚拟功能 (VF) 的微型端口驱动程序与 PCIe 物理功能 (PF) 之间提供通信通道或*backchannel*。 每个 VF 微型端口驱动程序都可以通过 backchannel 将请求发送到 PF 微型端口驱动程序。 PF 小型端口驱动程序可以通过 backchannel 将状态通知发送到单个 VF 微型端口驱动程序。

通过 backchannel 接口在 PF 和 VF 微型端口驱动程序之间交换的数据涉及使用*VF 配置块*。 每个 VF 配置块在概念上类似于进程间通信 (IPC) 消息, 其中每个块都有一个专用的格式、长度和块标识符。 独立硬件供应商 (IHV) 可以为 PF 和 VF 微型端口驱动程序定义一个或多个 VF 配置块。

本部分包括以下主题：

[来自 VF 微型端口驱动程序的 Backchannel 通信](backchannel-communication-from-a-vf-miniport-driver.md)

[来自 PF 微型端口驱动程序的 Backchannel 通信](backchannel-communication-from-the-pf-miniport-driver.md)

 

 





