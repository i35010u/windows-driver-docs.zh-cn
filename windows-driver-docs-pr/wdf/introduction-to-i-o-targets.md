---
title: I/O 目标简介
description: I/O 目标简介
keywords:
- I/o 目标 WDK KMDF，关于 i/o 目标
- I/o 目标对象 WDK KMDF
- 远程 i/o 目标 WDK KMDF
- 本地 i/o 目标 WDK KMDF
- 函数驱动程序 WDK KMDF
- 筛选器驱动程序 WDK KMDF
- 微型端口驱动程序 WDK KMDF
- 专用 i/o 目标 WDK KMDF
- I/o 目标 WDK KMDF，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdd0a966a1ddaa15cfbf3fc74621f098c131490a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803445"
---
# <a name="introduction-to-io-targets"></a>I/O 目标简介





当 [函数驱动程序](wdm-concepts-for-kmdf-drivers.md)、筛选器驱动程序或 [微型端口驱动程序](creating-kmdf-miniport-drivers.md) 收到 i/o 请求时，驱动程序可能会自行处理请求，或者可能需要其他驱动程序的帮助。 如果驱动程序需要帮助，则可以将请求转发到其他驱动程序，也可以创建一个或多个新的请求并将其发送到另一个驱动程序。

在 Kernel-Mode Driver Framework 中， *i/o 目标* 表示作为 i/o 请求目标的设备对象。 函数、筛选器或微型端口驱动程序可以使用 i/o 目标将 i/o 请求发送到另一个驱动程序。 这些驱动程序通常会将其 i/o 请求发送到驱动程序堆栈中的下一个较低版本的驱动程序。 因此，每个基于框架的函数、筛选器和微型端口驱动程序都具有每个设备的 *本地 i/o 目标* ，这是设备的下一个较低驱动程序。

有时，驱动程序必须将 i/o 请求发送到另一个目标--其他驱动程序堆栈的顶部，或者很少是发送驱动程序堆栈中的其他驱动程序。 因此，该框架还提供 *远程 i/o 目标*，这些目标包含除本地 i/o 目标外的所有 i/o 目标。

每个 i/o 目标都由 *i/o 目标对象* 表示。 每个 i/o 目标对象主要是一个队列，用于控制向目标设备对象发送请求的时间。 当驱动程序向 i/o 目标发送请求时，框架会将请求存储在队列中，直到它能够将请求传递给目标设备对象。

该框架支持 *一般 i/o* 目标和 *专用 i/o 目标*：

-   所有函数、筛选器和微型端口驱动程序都可以使用[一般 i/o 目标](general-i-o-targets.md)，但它们不支持任何特定于设备的特定数据格式。

-   专用 i/o 目标使函数、筛选器和微型端口驱动程序能够轻松发送需要特定于目标的特定数据格式的 i/o 请求。 目前，该框架为以下专用 i/o 目标提供支持：
    -   [USB i/o 目标](usb-i-o-targets.md)

如果框架提供的专用 i/o 目标支持设备的数据格式，则驱动程序应使用专用 i/o 目标。 否则，驱动程序应使用一般 i/o 目标。

 

 





