---
title: 将 I/O 请求发送到常规 I/O 目标
description: 将 I/O 请求发送到常规 I/O 目标
ms.assetid: 3fa897f5-2de8-484b-becb-c2de23fb5e8c
keywords:
- 常规 I/O 面向 WDK KMDF，I/O 将请求发送到
- 发送 I/O 请求 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a64acbc2d146aea7a6f13765b4cb62cb1224351d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567897"
---
# <a name="sending-io-requests-to-general-io-targets"></a>将 I/O 请求发送到常规 I/O 目标





您的驱动程序可以将 I/O 请求发送到常规 I/O 目标同步或异步。

如果驱动程序将以同步方式发送的 I/O 请求，驱动程序线程一次发送一个请求。 为每个请求才能完成再发送下一个等待线程。 此过程是以异步方式发送的 I/O 请求比简单得多。 如果它不会发送多个请求，并且系统或设备的性能不会减少您的驱动程序等待每个 I/O 请求时，您的驱动程序可以以同步方式发送 I/O 请求。

如果驱动程序以异步方式发送的 I/O 请求，驱动程序线程将发送每个请求，请求一旦准备好发送，而无需等待以前发送的请求数完成。 如果您的驱动程序必须处理多个 I/O 请求以短的时间段，可能不能允许您的驱动程序要等待的每个请求发送的下一个请求之前完成。 否则为可能会丢失数据或降低的驱动程序的设备，并且可能对整个系统的性能。

框架的 I/O 目标对象提供了您的驱动程序可以调用的方法的两个集： 一个设置为[同步发送的 I/O 请求](sending-i-o-requests-synchronously.md)和其他设置为[异步发送的 I/O 请求](sending-i-o-requests-asynchronously.md)。

对于每个这些方法，必须提供请求对象和一些缓冲空间。 可以使用这些方法可以将您的驱动程序收到一个其 I/O 队列中的请求转发或可创建和发送新请求。

 

 





