---
title: I/O 目标简介
description: I/O 目标简介
ms.assetid: 06ab7b3e-6b3e-4cfe-a7a6-17292300c472
keywords:
- I/O 面向 WDK KMDF 有关 I/O 目标
- I/O 目标对象 WDK KMDF
- 远程 I/O 面向 WDK KMDF
- 本地 I/O 面向 WDK KMDF
- 函数的 WDK KMDF 驱动程序
- 筛选器驱动程序 WDK KMDF
- 微型端口驱动程序 WDK KMDF
- 专用的 I/O 面向 WDK KMDF
- I/O 面向 WDK KMDF，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e7bae4b2e03d1253c6162b6c83efe435a2c7a18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542249"
---
# <a name="introduction-to-io-targets"></a>I/O 目标简介





当[功能驱动程序](wdm-concepts-for-kmdf-drivers.md)，筛选器驱动程序，或[微型端口驱动程序](creating-kmdf-miniport-drivers.md)接收的 I/O 请求，该驱动程序可能能够处理该请求本身或它可能需要其他驱动程序的帮助。 如果驱动程序需要协助，它可以将请求转发到另一个驱动程序，或者它可以创建一个或多个新的请求并将其发送到另一个驱动程序。

在内核模式驱动程序框架中， *I/O 目标*表示目标的 I/O 请求的设备对象。 函数、 筛选器或微型端口驱动程序可以使用 I/O 目标将 I/O 请求发送到另一个驱动程序。 这些驱动程序通常将其 I/O 请求发送到驱动程序堆栈中的下一步低驱动程序。 因此，每个基于框架的函数、 筛选和微型端口驱动程序都有*本地 I/O 目标*为每个设备，这是设备的下一步低驱动程序。

有时，驱动程序必须将 I/O 请求发送到不同目标-或顶部的不同驱动程序堆栈，很少，一些其他驱动程序中发送驱动程序堆栈。 因此，该框架还提供*远程 I/O 目标*，其中包含的所有 I/O 目标只是本地的 I/O 目标。

表示每个 I/O 目标*I/O 目标对象*。 每个 I/O 目标对象是主要的队列，可以控制何时进行请求传递到目标设备对象。 当驱动程序将请求发送到的 I/O 目标时，该框架存储在队列中请求，直到它可以将请求传递到目标设备对象。

框架支持同时*常规 I/O 目标*并*专用 I/O 目标*:

-   [常规 I/O 目标](general-i-o-targets.md)可以由所有函数、 筛选和微型端口驱动程序，但它们不支持任何特殊的、 特定于设备的数据格式。

-   专用的 I/O 目标启用方便地发送需要特殊的、 特定于目标的数据格式设置的 I/O 请求的函数、 筛选和微型端口驱动程序。 目前，框架将为以下专用 I/O 目标提供支持：
    -   [USB I/O 目标](usb-i-o-targets.md)

如果该框架提供了专门支持你的设备的数据格式的 I/O 目标，您的驱动程序应使用专用的 I/O 目标。 否则，该驱动程序应使用常规 I/O 目标。

 

 





