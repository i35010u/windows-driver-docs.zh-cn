---
title: PIO 技术
description: PIO 技术
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 37d3fc18bc54e46614d7e31227428f78adc79edc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829545"
---
# <a name="pio-techniques"></a>PIO 技术


在某些计算机的硬件体系结构上，从 CPU (中央处理单元) 到设备的数据传输是通过 (PIO) 的编程输入/输出来完成的。 使用 PIO 要求 CPU 等待传输数据，这可能会变得非常低效。 在大多数情况下，此技术已在 (DMA) 的直接内存访问中被替换，因为 DMA 可以将数据传输分配给硬件控制器，让 CPU 执行其他任务。

有关将缓存与 PIO 配合使用的信息，请参阅 [在 Pio 操作期间刷新缓存的数据](flushing-cached-data-during-pio-operations.md)。

 

 




