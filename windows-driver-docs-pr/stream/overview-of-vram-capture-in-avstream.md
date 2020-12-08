---
title: AVStream 中的 VRAM 捕获概述
description: AVStream 中的 VRAM 捕获概述
keywords:
- VRAM 捕获 WDK AVStream，关于 VRAM 捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ee9418eec477bc591b0c9e5038421084500d227
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834873"
---
# <a name="overview-of-vram-capture-in-avstream"></a>AVStream 中的 VRAM 捕获概述


为了支持捕获到 VRAM，供应商在 Windows Vista 显示器驱动程序堆栈中添加了功能。 具体而言，该供应商提供支持特定 KS 属性的以 pin 为中心的 AVStream 微型驱动程序。 尽管可以在显示微型端口驱动程序中包含 AVStream 功能，但 Microsoft 建议将微型驱动程序从属于显示微型端口驱动程序。 若要查看说明显示微型端口驱动程序如何适应 Windows Vista 显示器驱动程序堆栈的图表，请参阅 Windows Vista 显示器驱动程序模型体系结构主题。

本文档介绍如何实现此类单独的独立捕获微型驱动程序。

捕获驱动程序可以将数据发送到任何 DXVA2 感知下游筛选器，例如呈现器或编码器。

下图显示了 VRAM 启用捕获的 AVStream 微型驱动程序如何与显示微型端口驱动程序和其他模块交互。

![说明 vram 启用捕获的 avstream 微型驱动程序如何与显示微型端口驱动程序和其他模块交互的关系图](images/lddmcapturearchitectureoverview.gif)

 

 




