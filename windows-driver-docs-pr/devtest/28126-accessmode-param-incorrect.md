---
title: C28126
description: 警告 C28126 将 AccessMode 参数 ObReferenceObject * 应为 IRP >Irp->requestormode。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28126
ms.openlocfilehash: 636ac80ecbb05804d57027513d6382610c2d8bb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840417"
---
# <a name="c28126"></a>C28126


警告 C28126： ObReferenceObject 的 AccessMode 参数 \* 应为 IRP- &gt; irp->requestormode

在对 [**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)或 [**ObReferenceObjectByPointer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)的调用中，驱动程序为 *AccessMode* 参数传递 **UserMode** 或 **KernelMode** ，而不是使用 **Irp- &gt; irp->requestormode**。

驱动程序应使用 **&gt; irp->requestormode**，而不是指定 **UserMode** 或 **KernelMode**。 这使得内核模式 IRP 的发送方能够安全地提供内核模式句柄。

此警告适用于驱动程序堆栈中的顶层驱动程序。 对于所有其他驱动程序，你可以忽略或禁止显示此警告。

驱动程序堆栈中的顶层驱动程序应使用 **&gt; irp->requestormode**，而不是指定 **UserMode** 或 **KernelMode**。 这使得内核模式 IRP 的发送方能够安全地提供内核模式句柄。 堆栈中的所有其他驱动程序都应指定 **KernelMode**，这将跳过访问检查，并对顶级驱动程序的访问检查承担责任。

 

