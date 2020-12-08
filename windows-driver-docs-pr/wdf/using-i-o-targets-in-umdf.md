---
title: 在 UMDF 中使用 I/O 目标
description: 在 UMDF 中使用 I/O 目标
keywords:
- 用户模式驱动程序 WDK UMDF，i/o 目标
- UMDF WDK，i/o 目标
- User-Mode Driver Framework WDK，i/o 目标
- 基于框架的驱动程序 WDK UMDF，i/o 目标
- I/o 目标为 WDK UMDF
- 目标 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8fd036f0b59f440e793b76cb4a0676912ad3e79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838705"
---
# <a name="using-io-targets-in-umdf"></a>在 UMDF 中使用 I/O 目标


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当驱动程序收到 i/o 请求时，驱动程序可能能够自行处理请求，或者可能需要其他驱动程序的帮助。 如果驱动程序需要帮助，则可以将请求转发到其他驱动程序，也可以创建一个或多个新的请求并将其发送到另一个驱动程序。

基于 UMDF 的驱动程序使用 *i/o 目标* 将 i/o 请求发送到另一个驱动程序。 每个 i/o 目标都由 i/o 目标对象表示。 每个 i/o 目标对象主要是一个队列。 当驱动程序向 i/o 目标发送请求时，框架会将请求存储在队列中，直到它能够将请求传递到 i/o 目标。

该框架支持一般 i/o 目标和专用 i/o 目标：

-   所有 UMDF 驱动程序都可以使用[一般 i/o 目标](general-i-o-targets-in-umdf.md)，但它们不支持任何特定于设备的特定数据格式。

-   专用 i/o 目标使 UMDF 驱动程序能够发送 i/o 请求，这些请求需要特殊的特定于目标的数据格式。 目前，该框架为 [USB i/o 目标](usb-i-o-targets-in-umdf.md)提供支持。

如果框架提供的专用 i/o 目标支持设备的数据格式，则驱动程序应使用专用 i/o 目标。 否则，驱动程序应使用一般 i/o 目标。

 

 





