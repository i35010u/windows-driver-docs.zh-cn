---
title: 将 I/O 请求发送到常规 I/O 目标
description: 将 I/O 请求发送到常规 I/O 目标
keywords:
- 一般 i/o 目标 WDK KMDF，将 i/o 请求发送到
- 发送 i/o 请求 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b104b8130ab7898c6295bc17dc57e274e126b10f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821167"
---
# <a name="sending-io-requests-to-general-io-targets"></a>将 I/O 请求发送到常规 I/O 目标





驱动程序可以通过同步或异步方式将 i/o 请求发送到一般 i/o 目标。

如果驱动程序同步发送 i/o 请求，则驱动程序线程一次发送一个请求。 线程会等待每个请求完成，然后再发送下一个请求。 此过程比异步发送 i/o 请求更简单。 如果你的驱动程序未发送多个请求，并且当你的驱动程序等待每个 i/o 请求时未减少系统或设备性能，则你的驱动程序可以同步发送 i/o 请求。

如果驱动程序以异步方式发送 i/o 请求，则驱动程序线程将在请求准备就绪后发送每个请求，而无需等待之前发送的请求完成。 如果你的驱动程序必须在较短的时间内处理多个 i/o 请求，你可能无法允许驱动程序等待每个请求完成，然后再发送下一个请求。 否则，可能会丢失数据或降低驱动程序的设备（可能为整个系统）的性能。

框架的 i/o 目标对象提供两组驱动程序可调用的方法：一个设置为 [同步发送 i/o 请求](sending-i-o-requests-synchronously.md) ，另一个设置为 [异步发送 i/o 请求](sending-i-o-requests-asynchronously.md)。

对于上述每种方法，必须提供请求对象和某些缓冲区空间。 你可以使用这些方法来转发驱动程序在其一个 i/o 队列中接收的请求，或者创建并发送新请求。

 

 





