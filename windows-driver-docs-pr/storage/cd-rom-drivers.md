---
title: Cd-rom 驱动程序简介
description: CD-ROM 驱动程序
keywords:
- CD-ROM 驱动程序 WDK 存储
- 存储 cd-rom 驱动程序 WDK
- 存储驱动程序 WDK、cd-rom
- IOCTLs WDK cd-rom
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6171470d4b4564fd30395b0fd747478be9802f2e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811761"
---
# <a name="introduction-to-cd-rom-drivers"></a>Cd-rom 驱动程序简介

当操作系统枚举 CD-ROM 设备时，它将 (*Cdrom.sys*) 加载本机 cd-rom 类驱动程序。 此驱动程序 (IOCTL) 接口公开 i/o 控制请求。 Cd-rom 设备驱动程序的所有公共 i/o 控制代码均使用缓冲 i/o。 因此，这些请求的输入或输出数据位于 >AssociatedIrp.SystemBuffer 中。 有关详细信息，请参阅 cd-rom [i/o 控制代码](cd-rom-io-control-codes.md)

Cd-rom 设备的类驱动程序处理额外的公共 i/o 控制代码，以及本节所述的代码。 有关存储类驱动程序要求的详细信息，请参阅 [常规存储 I/o 控制代码](general-storage-io-control-codes.md)。

以下主题介绍了 CD-ROM 类驱动程序 IOCTL 接口的一些主要功能：

- [Cd-rom 独占访问](cd-rom-exclusive-access-mode.md)

- [CD-ROM 设置速度](cd-rom-set-speed.md)

- [CD-ROM 实时流式处理](cd-rom-real-time-streaming-.md)

- [ACL 和设备堆栈](acls-and-the-device-stack.md)
