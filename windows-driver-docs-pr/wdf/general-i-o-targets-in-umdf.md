---
title: UMDF 中的常规 I/O 目标
description: UMDF 中的常规 I/O 目标
ms.assetid: 46fac165-3afd-4481-b68d-8d3474e0ff52
keywords:
- 一般 i/o 目标为 WDK UMDF
- I/o 目标为 WDK UMDF，常规
- 本地 i/o 目标 WDK UMDF
- 远程 i/o 目标 WDK UMDF
- 一般 i/o 目标是有关一般 i/o 目标的 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5f01e28c9c1526df005dce70ada77977d0caff7
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209931"
---
# <a name="general-io-targets-in-umdf"></a>UMDF 中的常规 I/O 目标


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

一般 i/o 目标可以是*本地*的，也可以是*远程*的，它们是不支持特定于设备的特定数据格式（如 USB 请求块）的 i/o 目标。 在驱动程序将数据发送到一般 i/o 目标之前，必须使用 i/o 目标和设备可以解释的格式将数据置于写入缓冲区。 同样，当驱动程序从常规 i/o 目标读取数据时，驱动程序必须能够解释它们从目标接收的数据缓冲区的内容。

<a href="" id="local-i-o-targets-------"></a>**本地 I/o 目标**   
驱动程序通常将 i/o 请求发送到驱动程序堆栈中的下一个较低的驱动程序。 因此，每个基于 UMDF 的驱动程序都具有每个设备的*默认 i/o 目标*，这是设备的下一个较低驱动程序。 最低级别的基于 UMDF 的驱动程序的默认 i/o 目标是内核模式[反射](overview-of-the-umdf.md)器。

有时，基于 UMDF 的驱动程序必须将 i/o 请求发送到基于文件句柄的 i/o 目标，如文件或网络套接字。 因此，该框架还提供基于文件句柄的 i/o 目标对象。

默认 i/o 目标和基于文件句柄的 i/o 目标均称为*本地 i/o 目标*，因为基于 UMDF 的驱动程序使用这些目标向驱动程序堆栈支持的设备发送 i/o 请求。

<a href="" id="remote-i-o-targets-------"></a>**远程 I/o 目标**   
有时，驱动程序必须将 i/o 请求发送到不同的驱动程序堆栈。 因此，该框架还提供*远程 i/o 目标*，这些目标包含除本地 i/o 目标外的所有 i/o 目标。

远程 i/o 目标可能是驱动程序堆栈不支持的设备、该设备上的文件或设备的[设备接口](using-device-interfaces-in-umdf-drivers.md)。

以下各节介绍如何初始化和使用一般 i/o 目标：

-   [在 UMDF 中初始化常规 i/o 目标](initializing-a-general-i-o-target-in-umdf.md)
-   [在 UMDF 中将 i/o 请求发送到一般 i/o 目标](sending-i-o-requests-to-a-general-i-o-target-in-umdf.md)
-   [在 UMDF 中控制常规 i/o 目标的状态](controlling-a-general-i-o-target-s-state-in-umdf.md)
-   [获取有关 UMDF 中常规 i/o 目标的信息](obtaining-information-about-a-general-i-o-target-in-umdf.md)

 

 





