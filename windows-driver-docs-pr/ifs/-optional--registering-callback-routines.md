---
title: 可有可无注册回调例程
description: 可有可无注册回调例程
keywords:
- 注册回调例程
- 回调例程 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecfa96ecd102de769c1feb8a802179b57ae28d26
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789977"
---
# <a name="optional-registering-callback-routines"></a>\[可选 \] 注册回调例程


## <span id="ddk_registering_callback_routines_if"></span><span id="DDK_REGISTERING_CALLBACK_ROUTINES_IF"></span>


筛选器驱动程序可以调用 [**IoRegisterFsRegistrationChange**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfsregistrationchange) ，以便在每次文件系统驱动程序调用 [**IoRegisterFileSystem**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem) 或 [**IoUnregisterFileSystem**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iounregisterfilesystem) 来注册或取消注册时调用回调例程。 筛选器驱动程序注册此回调例程，使其可以看到新文件系统输入系统，并选择是否附加到它们。

**注意**   文件系统筛选器驱动程序绝不能调用 [**IoRegisterFileSystem**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem) 或 [**IoUnregisterFileSystem**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iounregisterfilesystem)。 这些例程仅适用于文件系统。

 

仅当显式定向 (（例如，用户模式应用程序) 不应调用 [**IoRegisterFsRegistrationChange**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfsregistrationchange)的情况下，才筛选仅附加到卷的驱动程序）。 但请注意，使用此例程的筛选器可以在装入该卷后立即附加到任何指定的卷。 使用此例程不保证筛选器将直接附加到卷设备对象。 但它确实可以确保在 (之前附加此类筛选器，因此) 从用户模式应用程序等待命令的任何筛选器，因为筛选器只能附加在当前文件系统卷设备堆栈的顶部。

 

