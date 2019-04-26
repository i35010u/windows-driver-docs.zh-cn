---
title: 在 UMDF 中使用 I/O 目标
description: 在 UMDF 中使用 I/O 目标
ms.assetid: 5633242c-ffab-4af5-9650-7449395deb6b
keywords:
- 用户模式驱动程序 WDK UMDF，I/O 目标
- UMDF WDK，I/O 目标
- 用户模式驱动程序框架 WDK，I/O 目标
- 基于框架的驱动程序 WDK UMDF，I/O 目标
- I/O 面向 WDK UMDF
- 针对 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd8ac3b30b27d7c568dcc8cb5395bcfbab6aa028
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327161"
---
# <a name="using-io-targets-in-umdf"></a>在 UMDF 中使用 I/O 目标


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

驱动程序接收的 I/O 请求，该驱动程序可能能够处理该请求本身，或可能还需要其他驱动程序的帮助。 如果驱动程序需要协助，它可以将请求转发到另一个驱动程序，或者它可以创建一个或多个新的请求并将其发送到另一个驱动程序。

基于 UMDF 驱动程序使用*I/O 目标*将 I/O 请求发送到另一个驱动程序。 每个 I/O 目标为由 I/O 目标对象。 每个 I/O 目标对象是主要队列。 当驱动程序将请求发送到的 I/O 目标时，该框架存储在队列中请求，直到它可以将请求传递到 I/O 目标。

框架支持常规 I/O 目标和专用的 I/O 目标：

-   [常规 I/O 目标](general-i-o-targets-in-umdf.md)可以由所有 UMDF 驱动程序，但它们不支持任何特殊的、 特定于设备的数据格式。

-   专用的 I/O 目标启用 UMDF 驱动程序发送需要特殊的、 特定于目标的数据格式设置的 I/O 请求。 目前，该框架提供的支持[USB I/O 目标](usb-i-o-targets-in-umdf.md)。

如果该框架提供了专门支持你的设备的数据格式的 I/O 目标，您的驱动程序应使用专用的 I/O 目标。 否则，该驱动程序应使用常规 I/O 目标。

 

 





