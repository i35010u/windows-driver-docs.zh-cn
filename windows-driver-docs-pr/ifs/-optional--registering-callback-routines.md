---
title: 可有可无注册回调例程
description: 可有可无注册回调例程
ms.assetid: 59d15b37-e31e-45fc-bdb0-fed6f791839c
keywords:
- 注册回调例程
- 回调例程 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeb9552cd4a9985fdd6c37f258a848f8f1ef1ab2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841518"
---
# <a name="optional-registering-callback-routines"></a>注册回调例程 \[可选\]


## <span id="ddk_registering_callback_routines_if"></span><span id="DDK_REGISTERING_CALLBACK_ROUTINES_IF"></span>


筛选器驱动程序可以调用[**IoRegisterFsRegistrationChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfsregistrationchange) ，以便在每次文件系统驱动程序调用[**IoRegisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem)或[**IoUnregisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iounregisterfilesystem)来注册或取消注册时调用回调例程。 筛选器驱动程序注册此回调例程，使其可以看到新文件系统输入系统，并选择是否附加到它们。

**注意**   文件系统筛选器驱动程序不能调用[**IoRegisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem)或[**IoUnregisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iounregisterfilesystem)。 这些例程仅适用于文件系统。

 

仅当显式定向时（例如，用户模式应用程序）不应调用[**IoRegisterFsRegistrationChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfsregistrationchange)的筛选器的筛选器。 但请注意，使用此例程的筛选器可以在装入该卷后立即附加到任何指定的卷。 使用此例程不保证筛选器将直接附加到卷设备对象。 但它确实可以确保这样的筛选器会附加到从用户模式应用程序等待命令的任何筛选器之前（及其下），因为筛选器只能附加在当前文件系统卷设备堆栈的顶部。

 

 




