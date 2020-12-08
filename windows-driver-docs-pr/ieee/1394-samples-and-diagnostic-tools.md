---
title: 1394 示例和诊断工具
description: 1394 示例和诊断工具
keywords:
- IEEE 1394 WDK 总线，示例
- 1394 WDK 总线，示例
- IEEE 1394 WDK 总线，诊断工具
- 1394 WDK 总线，诊断工具
- 示例驱动程序 WDK IEEE 1394 总线
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93d68a09e3addc83b0db5e65aeedd65882578013
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794965"
---
# <a name="1394-samples-and-diagnostic-tools"></a>1394 示例和诊断工具


Windows 驱动程序工具包 (WDK) 包含两个示例内核模式驱动程序的源代码 (*1394vdev.sys* 和 *1394diag.sys*) 和诊断软件，它们允许驱动程序编写者从用户模式与 IEEE 1394 堆栈进行通信。

驱动程序源代码说明了驱动程序如何与 IEEE 1394 堆栈的上边缘通信。 除了异步和同步数据传输外，示例源代码还演示了如何正确管理即插即用 (PnP) 和电源管理 i/o 请求数据包 (Irp) 。

系统将枚举 *1394vdev.sys* ，并以不同方式 *1394diag.sys* 。 1394vdev.sys 驱动程序是一个虚拟诊断驱动程序，IEEE 1394 总线驱动程序在收到 IOCTL \_ IEEE1394 \_ API \_ 请求请求时会加载该驱动程序。 *1394diag.sys* 驱动程序是一个物理诊断设备驱动程序，ieee 1394 总线驱动程序会在将 ieee 1394 硬件设备插入 PC 时加载该驱动程序。 *1394vdev* 包含在 WDK 中，同时加载这两个驱动程序。

 

 




