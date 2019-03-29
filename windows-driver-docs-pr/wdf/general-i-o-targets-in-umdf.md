---
title: UMDF 中的常规 I/O 目标
description: UMDF 中的常规 I/O 目标
ms.assetid: 46fac165-3afd-4481-b68d-8d3474e0ff52
keywords:
- 常规 I/O 面向 WDK UMDF
- I/O 面向 WDK UMDF，常规
- 本地 I/O 面向 WDK UMDF
- 远程 I/O 面向 WDK UMDF
- 常规 I/O 有关常规 I/O 目标面向 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d35cd8b7f8d79eec794211b7211411cd59ef8c98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565232"
---
# <a name="general-io-targets-in-umdf"></a>UMDF 中的常规 I/O 目标


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

常规 I/O 目标，可以是*本地*或*远程*，是不支持特殊的、 特定于设备的数据格式，例如 USB 请求块的 I/O 目标。 驱动程序将数据发送到常规 I/O 目标之前，它们必须将数据放入 I/O 目标和设备可以解释的格式写入缓冲区。 同样，当驱动程序从常规 I/O 目标中读取数据，驱动程序必须能够解释它们接收来自目标的数据缓冲区的内容。

<a href="" id="local-i-o-targets-------"></a>**本地 I/O 目标**   
驱动程序通常将 I/O 请求发送到驱动程序堆栈中的下一步低驱动程序。 因此，每个基于 UMDF 驱动程序都有*默认 I/O 目标*为每个设备，这是设备的下一步低驱动程序。 最低级别 UMDF 驱动程序的默认 I/O 目标是内核模式[reflector](overview-of-the-umdf.md)。

有时基于 UMDF 驱动程序必须将 I/O 请求发送到一个基于文件的句柄的 I/O 目标，如文件或网络套接字。 因此，该框架还提供基于文件句柄的 I/O 目标对象。

调用默认 I/O 目标和基于文件句柄的 I/O 目标*本地 I/O 目标*，因为基于 UMDF 驱动程序使用这些目标将 I/O 请求发送到设备的驱动程序堆栈支持。

<a href="" id="remote-i-o-targets-------"></a>**远程 I/O 的目标**   
有时，驱动程序必须将 I/O 请求发送到不同驱动程序堆栈。 因此，该框架还提供*远程 I/O 目标*，其中包含的所有 I/O 目标除本地 I/O 目标。

远程 I/O 目标可能是驱动程序堆栈不支持，该设备上的文件的设备或[设备接口](using-device-interfaces-in-umdf-drivers.md)为该设备。

以下部分介绍如何初始化和使用常规 I/O 目标：

-   [初始化 UMDF 中的常规 I/O 目标](initializing-a-general-i-o-target-in-umdf.md)
-   [将 I/O 请求发送到 UMDF 中的常规 I/O 目标](sending-i-o-requests-to-a-general-i-o-target-in-umdf.md)
-   [控制在 UMDF 常规 I/O 目标的状态](controlling-a-general-i-o-target-s-state-in-umdf.md)
-   [获取有关 UMDF 中的常规 I/O 目标的信息](obtaining-information-about-a-general-i-o-target-in-umdf.md)

 

 





