---
title: 常规 I/O 目标
description: 常规 I/O 目标
keywords:
- 一般 i/o 目标 WDK KMDF
- I/o 目标 WDK KMDF，常规
- 本地 i/o 目标 WDK KMDF
- 远程 i/o 目标 WDK KMDF
- 一般 i/o 目标 WDK KMDF，关于一般 i/o 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05c82e5d80b5a09ee65b4b7e304a81b5f6bda0c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814760"
---
# <a name="general-io-targets"></a>常规 I/O 目标





一般 i/o 目标不支持特定于设备的特殊数据格式，如 USB 请求块。 在驱动程序将数据发送到一般 i/o 目标之前，必须使用 i/o 目标可以解释的格式将数据置于写入缓冲区。 同样，当驱动程序从常规 i/o 目标读取数据时，驱动程序必须能够解释它们从目标接收的数据缓冲区的内容。

一般 i/o 目标为本地或远程：

<a href="" id="local-i-o-targets"></a>本地 i/o 目标  
每个基于框架的函数驱动程序、筛选器驱动程序和微型端口驱动程序都具有每个驱动程序设备的本地 i/o 目标。 设备的本地 i/o 目标总是驱动程序堆栈中的下一个低驱动程序。

<a href="" id="remote-i-o-targets"></a>远程 i/o 目标  
远程 i/o 目标表示不同驱动程序堆栈的顶部，或 (很少) 当前驱动程序堆栈中的其他驱动程序。

本节包括：

-   [初始化常规 I/O 目标](initializing-a-general-i-o-target.md)

-   [将 I/O 请求发送到常规 I/O 目标](sending-i-o-requests-to-general-i-o-targets.md)

-   [控制常规 I/O 目标的状态](controlling-a-general-i-o-target-s-state.md)

-   [获取有关常规 I/O 目标的信息](obtaining-information-about-a-general-i-o-target.md)

 

 





