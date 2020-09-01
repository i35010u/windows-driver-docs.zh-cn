---
title: 扫描到可调谐信号
description: 扫描到可调谐信号
ms.assetid: cc934079-5d00-42e0-a024-1b7548bb88e4
keywords:
- 扫描 WDK 视频捕获信号
- 扫描可调式信号音频捕获
- 可调式信号音频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4b06cba49ebd5df0d116c8410d5915d471f64ca
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186311"
---
# <a name="scanning-to-tunable-signals"></a>扫描到可调谐信号


**本部分仅适用于从 Microsoft Windows Vista 开始的操作系统。**

信号扫描是指锁定到下一个可调式信号的过程， (按电缆或天线系统上的一系列频率值广播) 。 对于 Windows Vista 之前的操作系统，信号扫描主要由 *KsTvTune.ax*) 模块 (软件驱动，并基于扫描信道的已知地图，而不是对广播频谱进行基于频率的扫描。 如果在 Windows Vista 上运行的 AVStream 微型驱动程序在 [PROPSETID \_ 调谐器](./propsetid-tuner.md) 属性集中通过 windows vista 的新的 windows vista 属性报告了信号扫描功能，则调谐器筛选器 (*KsTvTune.ax*) 并且上述应用程序可以使用这些功能进行扫描。 如果驱动程序不支持新的基于频率的扫描功能， *KsTvTune.ax* 将回退到以前基于通道的扫描功能。

调谐器筛选器和 AVStream 微型驱动程序可以通过使用 [硬件辅助扫描算法](hardware-assisted-scanning-algorithm.md)来处理新的基于频率的扫描功能。

扫描完成后，微型驱动程序必须发出事件句柄的信号。 有关事件操作流的信息，请参阅 [事件机制和流](event-mechanism-and-flow.md)。

若要支持新的基于频率的扫描功能，微型驱动程序必须实现以下列表中的必需属性，还可以选择实现其余属性和事件：

[**KSPROPERTY \_需要 (调谐器 \_ 扫描 \_ 端**](./ksproperty-tuner-scan-caps.md)) 

[**KSPROPERTY \_调谐器 \_ 扫描 \_ 状态**](./ksproperty-tuner-scan-status.md) (可选) 

[**KSPROPERTY \_调谐器 \_ NETWORKTYPE \_ SCAN \_ cap**](./ksproperty-tuner-networktype-scan-caps.md) (可选) 

[**KSEVENT \_调谐器 \_ 启动 \_ 扫描**](./ksevent-tuner-initiate-scan.md) (可选) 

 

