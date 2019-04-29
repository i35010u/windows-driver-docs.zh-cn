---
title: 常规 I/O 目标
description: 常规 I/O 目标
ms.assetid: e5527aa2-a63f-49d8-aa9a-f91efd2ae9ad
keywords:
- 常规 I/O 面向 WDK KMDF
- I/O 面向 WDK KMDF，常规
- 本地 I/O 面向 WDK KMDF
- 远程 I/O 面向 WDK KMDF
- 常规 I/O 面向 WDK KMDF 有关常规 I/O 目标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05e5f456965913d030ee3c86b3eb272c856e9c67
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378120"
---
# <a name="general-io-targets"></a>常规 I/O 目标





常规 I/O 目标不支持特殊的、 特定于设备的数据格式，例如 USB 请求块。 驱动程序将数据发送到常规 I/O 目标之前，它们必须将数据放入 I/O 目标可以解释的格式写入缓冲区。 同样，当驱动程序从常规 I/O 目标中读取数据，驱动程序必须能够解释它们接收来自目标的数据缓冲区的内容。

常规 I/O 目标为本地或远程：

<a href="" id="local-i-o-targets"></a>本地 I/O 目标  
每个基于框架的功能驱动程序、 筛选器驱动程序和微型端口驱动程序都有一个本地的 I/O 目标为每个驱动程序的设备。 设备的本地 I/O 目标始终是驱动程序堆栈中的下一步低驱动程序。

<a href="" id="remote-i-o-targets"></a>远程 I/O 的目标  
远程 I/O 目标表示不同的驱动程序堆栈或 （很少） 当前驱动程序的堆栈中的不同驱动程序的顶部。

本部分包括：

-   [初始化常规 I/O 目标](initializing-a-general-i-o-target.md)

-   [将 I/O 请求发送到常规 I/O 目标](sending-i-o-requests-to-general-i-o-targets.md)

-   [控制常规 I/O 目标状态](controlling-a-general-i-o-target-s-state.md)

-   [获取有关常规 I/O 目标的信息](obtaining-information-about-a-general-i-o-target.md)

 

 





