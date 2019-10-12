---
title: 使用有保证的协定 DMA 缓冲区模型
description: 使用有保证的协定 DMA 缓冲区模型
ms.assetid: fee6f7eb-157b-466d-b482-110a48045283
keywords:
- DMA 缓冲区 WDK 显示，保证协定模式
- 保证协定 DMA 缓冲区 WDK 显示
- 修补程序-位置列表 WDK 显示
ms.date: 10/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: e62bcabe753a0c92422e326422076ab71b7c77bf
ms.sourcegitcommit: d57f3ad976393a2c5dffc05851a0314858ce05e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2019
ms.locfileid: "72280264"
---
# <a name="using-the-guaranteed-contract-dma-buffer-model"></a>使用有保证的协定 DMA 缓冲区模型

Windows Vista 的显示驱动程序模型可保证呈现设备的 DMA 缓冲区大小和修补程序位置列表。 修补程序位置列表包含 DMA 缓冲区中的命令所引用资源的物理内存地址。

在确保协定模式下，用户模式显示驱动程序可以识别 DMA 缓冲区和修补程序位置列表的准确大小，当用户模式显示驱动程序填充命令缓冲区并调用[**pfnRenderCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)将其提交到显示微型端口驱动程序。 对**pfnRenderCb**的每次调用后，用户模式显示驱动程序将接收可用于以下转换的 DMA 缓冲区和修补位置列表的大小（即，对**pfnRenderCb**的以下调用）。

在下一次转换完成之前，视频内存管理器保证不要为该设备剪裁 DMA 缓冲区和修补程序位置列表。 显示微型端口驱动程序必须能够将一个命令缓冲区转换成恰好一个 DMA 缓冲区和一个修补程序位置列表。 如果无法转换，则用户模式命令缓冲区按定义无效。 显示微型端口驱动程序无法返回在转换过程中指明它不在 DMA 缓冲区空间和修补程序位置的状态。这样做会导致视频内存管理器 bug 检查系统，因为内存管理器未能满足确保 DMA 协定的要求。
