---
title: CD-ROM 驱动程序
description: CD-ROM 驱动程序
ms.assetid: 04b0a605-7816-4804-bfa8-39122a03ce16
keywords:
- CD-ROM 驱动程序 WDK 存储
- 存储 CD-ROM 驱动程序 WDK
- 存储驱动程序 WDK、 CD-ROM
- Ioctl WDK CD-ROM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 473785555fd63c98ea2cb111c4a0ffd503bffc68
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348467"
---
# <a name="cd-rom-drivers"></a>CD-ROM 驱动程序

以下主题介绍一些 IOCTL 接口的主要功能：

[CD-ROM 独占访问](cd-rom-exclusive-access-mode.md)

[CD-ROM 设置的速度](cd-rom-set-speed.md)

[CD-ROM 实时流式处理](cd-rom-real-time-streaming-.md)

[Acl 和设备堆栈](acls-and-the-device-stack.md)

时操作系统枚举 CD-ROM 设备时，它会加载本机 CD-ROM 类驱动程序 (*Cdrom.sys*)。 此驱动程序公开一个 I/O 控制 (IOCTL) 请求接口。 所有公共的 I/O 控制代码的 CD-ROM 的设备驱动程序使用缓冲的 I/O。 因此，输入或输出数据的这些请求位于 Irp-> AssociatedIrp.SystemBuffer。 有关详细信息，请参阅[CD-ROM I/O 控制代码](cd-rom-io-control-codes.md)

CD-ROM 设备的类驱动程序处理其他公共 I/O 控制代码，以及与那些在本部分中所述。 有关存储类驱动程序要求的详细信息，请参阅[常规存储 I/O 控制代码](general-storage-io-control-codes.md)。