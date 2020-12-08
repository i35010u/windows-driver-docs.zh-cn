---
title: 主要 I/O 路径
description: 主要 I/O 路径
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de9e65aff11abe55749a803699ac4c5918765e15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835053"
---
# <a name="main-io-path"></a>主要 I/O 路径


Storport 提供的一项体系结构改进是 HwBuildIo 例程。 尽管此 Storport 微型端口驱动程序入口点是可选的，但强烈建议这样做。 LSI \_ U3 驱动程序通过实现 LsiU3BuildIo 例程来利用此改进。 此入口点在未持有任何锁的 HwStartIo 例程之前调用，只要不修改共享内存，此例程就可能会执行之前在 HwStartIo 例程中完成的处理（对于基于 Scsiport 的微型端口驱动程序）。 这允许在多处理器系统上并行执行所需的大多数处理，以启动单独的 i/o 请求。

LsiU3StartIo 例程将驱动程序队列标记分配给 i/o 请求。 这是必需的，因为 Storport 基于每个 LUN 分配队列标记，而不是基于每个适配器。 适配器硬件的最大限制为256个未完成 i/o。

 

 




