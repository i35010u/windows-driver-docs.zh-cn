---
title: 1394 示例和诊断工具
description: 1394 示例和诊断工具
ms.assetid: e3ce71da-8c24-405b-b734-98a8c4f45e6b
keywords:
- IEEE 1394 WDK 总线示例
- 1394 WDK 总线示例
- IEEE 1394 WDK 总线，诊断工具
- 1394 WDK 总线，诊断工具
- 示例驱动程序 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca81ef6ad9e515ed8600a700a4ab664853d04346
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376710"
---
# <a name="1394-samples-and-diagnostic-tools"></a>1394 示例和诊断工具


Windows Driver Kit (WDK) 包括两个示例内核模式驱动程序的源代码 (*1394vdev.sys*并*1394diag.sys*) 和诊断允许驱动程序编写人员与进行通信的软件从用户模式下的 IEEE 1394 堆栈。

驱动程序源代码说明了驱动程序的 IEEE 1394 堆栈的上边缘与通信的方式。 除了异步和同步数据传输，示例源代码演示适当管理插即用 (PnP) 和电源管理 I/O 请求数据包 (Irp)。

系统枚举*1394vdev.sys*并*1394diag.sys*以不同的方式。 1394vdev.sys 驱动程序是一个虚拟的诊断驱动程序的 IEEE 1394 总线驱动程序加载时收到 IOCTL\_IEEE1394\_API\_请求请求。 *1394diag.sys*驱动程序是 IEEE 1394 硬件设备插入到 PC 时，将加载 IEEE 1394 总线驱动程序诊断的物理设备驱动程序。 *1394vdev.inf*，WDK 中包含的加载这两个这些驱动程序。

 

 




