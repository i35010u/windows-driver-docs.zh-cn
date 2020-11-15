---
title: 访问用户空间内存
description: 访问用户空间内存
ms.assetid: db0b6ba2-4cec-46c1-b13f-aba4c10a2d8c
keywords:
- 内存管理 WDK 内核，用户空间内存
- 用户空间内存 WDK 内核
- 虚拟用户空间内存 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e17fc2d14ee248a3907cecb8ae9b276db224c45f
ms.sourcegitcommit: 774cca93409062c813143c8dc4c55f5c883d2b1a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2020
ms.locfileid: "94634635"
---
# <a name="accessing-user-space-memory"></a>访问用户空间内存


驱动程序无法通过用户模式虚拟地址直接访问内存，除非它在导致驱动程序当前 i/o 操作的用户模式线程的上下文中运行，并且使用该线程的虚拟地址。

只有最上层的驱动程序（如 FSDs）才能确保在此类用户模式线程的上下文中调用其调度例程。 最高级别的驱动程序可以调用 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) 来锁定用户缓冲区，然后再为较低版本的驱动程序设置 IRP。

为 [缓冲 i/o](methods-for-accessing-data-buffers.md) 或 [直接 i/o](methods-for-accessing-data-buffers.md) 设置其设备对象的最低级别和中间驱动程序可以依赖于 i/o 管理器或最高级别的驱动程序，以将有效访问权限传递到锁定用户缓冲区或 irp 中的系统空间缓冲区。

 

