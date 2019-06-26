---
title: 扫描到可调谐信号
description: 扫描到可调谐信号
ms.assetid: cc934079-5d00-42e0-a024-1b7548bb88e4
keywords:
- 扫描 WDK 视频捕获的信号
- 扫描可优化信号 WDK 视频捕获
- 可优化信号 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc89b92cfb080464f8f3a4722d477fe6fbe35a47
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358424"
---
# <a name="scanning-to-tunable-signals"></a>扫描到可调谐信号


**本部分仅适用于与 Microsoft Windows Vista 一起启动的操作系统。**

信号扫描是广播沿电缆或天线的系统上的频率值的范围的锁定到下一个可优化信号 （增加或缩减） 过程。 有关操作系统前面比 Windows Vista 中，发出信号扫描很大程度上由软件驱动 ( *KsTvTune.ax*模块) 和基于扫描而不是基于频率的广播范围扫描的通道的已知的映射。 如果在 Windows Vista 运行 AVStream 微型驱动程序报告回信号扫描功能通过新的 Windows Vista 中的属性[PROPSETID\_调谐器](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-tuner)属性集，调谐器筛选器 (*KsTvTune.ax*) 和更高版本的应用程序可以使用这些功能进行扫描。 如果该驱动程序不支持的新基于频率的扫描功能， *KsTvTune.ax*回退到以前的基于通道的扫描功能。

调谐器筛选器和 AVStream 微型驱动程序可以通过使用来处理新的基于频率的扫描功能[硬件辅助扫描算法](hardware-assisted-scanning-algorithm.md)。

扫描完成时，微型驱动程序必须发出信号的事件句柄。 有关事件的操作流的信息，请参阅[事件机制和 Flow](event-mechanism-and-flow.md)。

为支持新的基于频率的扫描功能，微型驱动程序必须实现以下列表中的所需的属性并可以选择实现的其余属性和事件：

[**KSPROPERTY\_调谐器\_扫描\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-caps) （必需）

[**KSPROPERTY\_调谐器\_扫描\_状态**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-scan-status) （可选）

[**KSPROPERTY\_调谐器\_NETWORKTYPE\_扫描\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-tuner-networktype-scan-caps) （可选）

[**KSEVENT\_调谐器\_启动\_扫描**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-tuner-initiate-scan) （可选）

 

 




