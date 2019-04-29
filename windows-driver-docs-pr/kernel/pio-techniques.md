---
title: PIO 技术
description: PIO 技术
ms.assetid: bd673e43-c864-416b-b0d0-23c4ba1b870c
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fd5f6a1a9051d8b2bbc0178807a38ceabe24ae5f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369255"
---
# <a name="pio-techniques"></a>PIO 技术


在某些计算机硬件体系结构，数据 CPU （中央处理单元） 传输到设备可通过编程输入/输出 (PIO)。 使用 PIO 需要 CPU 等待数据传输，这可能会变得非常低效。 此技术已更换在大多数情况下通过直接内存访问 (DMA) 因为 DMA 可以分配的数据传输到硬件控制器，允许执行其他任务的 CPU。

通过 PIO 使用缓存的信息，请参阅[刷新缓存数据在 PIO 操作期间](flushing-cached-data-during-pio-operations.md)。

 

 




