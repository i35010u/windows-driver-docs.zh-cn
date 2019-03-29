---
title: AVStream 中的 VRAM 捕获概述
description: AVStream 中的 VRAM 捕获概述
ms.assetid: b5fd026f-75e3-49e0-a39e-4883dd6cacf2
keywords:
- 有关 vram 能够捕获的 vram 能够捕获 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad7d9f7aa5cc9a24fb7fdd11d4a264f93cd783c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561976"
---
# <a name="overview-of-vram-capture-in-avstream"></a>AVStream 中的 VRAM 捕获概述


若要支持 vram 能够捕获，供应商将添加 Windows Vista 显示驱动程序堆栈中的功能。 具体而言，由供应商提供的 pin 以中心 AVStream 微型驱动程序支持特定 KS 属性。 虽然可能包括显示微型端口驱动程序中的 AVStream 功能，但 Microsoft 建议微型驱动程序改为从属于显示微型端口驱动程序。 若要查看关系图，说明如何显示微型端口驱动程序适用于 Windows Vista 显示驱动程序堆栈，请转到 Windows Vista 显示驱动程序模型体系结构主题。

本文档介绍如何实现这种单独的独立捕获微型驱动程序。

捕获驱动程序可以发送到任何 DXVA2 可识别的下游数据筛选，例如，呈现器或编码器。

下图显示了 vram 能够捕获启用 AVStream 微型驱动程序与显示微型端口驱动程序和其他模块的交互。

![说明 vram 能够捕获启用 avstream 微型驱动程序如何与显示微型端口驱动程序和其他模块进行交互的关系图](images/lddmcapturearchitectureoverview.gif)

 

 




