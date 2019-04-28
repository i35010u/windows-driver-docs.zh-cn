---
title: 主要 I/O 路径
description: 主要 I/O 路径
ms.assetid: 643842e4-a75e-4d86-a1f7-d1a4468b5e17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5addbfc40365043d8cfed8f03674968192b7cca9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355571"
---
# <a name="main-io-path"></a>主要 I/O 路径


Storport 必须要提供的体系结构改进之一是 HwBuildIo 例程。 尽管此 Storport 微型端口驱动程序入口点是可选的我们强烈建议。 LSI\_U3 驱动程序通过实现 LsiU3BuildIo 例程来充分利用此项改进。 无锁 HwStartIo 例程保留，并且此例程，只要修改未共享的内存时，可能会在 HwStartIo 例程在基于 Scsiport 的微型端口驱动程序的情况下执行之前执行的处理之前调用此入口点。 这允许大部分所需启动单独的 I/O 请求，以同时在多处理器系统上执行的处理。

LsiU3StartIo 例程将驱动程序队列标记分配给输入/输出请求。 这需要，因为 Storport 分配每个 LUN 基础，而不是为每个适配器基础上的队列标记。 适配器硬件被限制为最多为 256 的未完成 I/o。

 

 




