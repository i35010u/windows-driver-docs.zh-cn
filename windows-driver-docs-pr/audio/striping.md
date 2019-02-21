---
title: 条带化
description: 条带化
ms.assetid: 29ab650c-0c3b-4693-a277-4d9ba63b7b66
keywords:
- 条带化 WDK 音频
- HD Audio，条带化
- 高清晰度音频 (HD Audio)，条带化
- HD Audio、 带宽
- 高清晰度音频 (HD Audio)、 带宽
- 总线带宽 WDK 音频
- 带宽 WDK 音频
- 分配的带宽
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a34f3d0baf0dad0b45fce80000c9d40379786ebd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534210"
---
# <a name="striping"></a>条带化


HD Audio 体系结构支持一种称为技术*条带化*，可以减少呈现流的总线带宽的使用。 如果高清晰度音频硬件接口提供了多个 SDO 行，条带化可以提高的渲染 DMA 引擎可将数据传输或者分布在 SDO 行之间的数据流中的位速率。 第一位 （最高有效位） 上 SDO0 传送时，通过 SDO1，等传输的第二位。 例如，两个 SDO 行，条带化，有效地提高一倍的传输速率通过拆分两个 SDO 行之间的流。 使用条带化以传输呈现流在两个 SDO 行的 DMA 引擎使用的只完成了一半总线带宽就会消耗如果未使用条带化。

函数驱动程序，通过条带化[ **AllocateRenderDmaEngine** ](https://msdn.microsoft.com/library/windows/hardware/ff536181)例程的*stripe*调用参数。

条带化的详细信息，请参阅*Intel 高定义音频规范*处[Intel HD Audio](https://go.microsoft.com/fwlink/p/?linkid=42508)网站。

 

 




