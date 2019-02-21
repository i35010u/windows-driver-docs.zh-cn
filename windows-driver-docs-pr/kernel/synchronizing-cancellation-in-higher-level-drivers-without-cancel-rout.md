---
title: 同步而无需取消例程的更高级别的驱动程序中的取消操作
description: 同步而无需取消例程的更高级别的驱动程序中的取消操作
ms.assetid: 741d504e-7e61-4f60-a8cf-e4ea92f0654e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5d71b962278ea66de32d11639848f8bd78d5b3e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534275"
---
# <a name="synchronizing-cancellation-in-higher-level-drivers-without-cancel-routines"></a>同步而无需取消例程的更高级别的驱动程序中的取消操作





更高级别的驱动程序可以做任何假设还是较低级别的现有驱动程序处理可取消 Irp 的方式。 只要任何更高级别的驱动程序调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)的 IRP，它不再拥有的 IRP 和它不能确定或控制处理的 IRP 的较低级驱动程序。

但是，可以设置任何更高级别的驱动程序[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程对于通过调用 IRP [ **IoSetCompletionRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549679)之前调用**IoCallDriver**。 更高级别的驱动程序可以确定是否任何挂起的 IRP 取消较低的驱动程序中通过调用**IoSetCompletionRoutine**与*InvokeOnCancel*参数设置为**TRUE**它将传递到较低的驱动程序 IRP 之前。 这样做可确保该驱动程序的*IoCompletion* IRP 是取消还是已完成，将调用例程。

更高级别的驱动程序可以调用[ **IoCancelIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548338)具有任何挂起的 IRP 已经分配了该驱动程序。 但是，进行此调用不能确保将状态设置为其 I/O 状态块已完成驱动程序分配 IRP\_已取消; 另一个线程可能已完成 IRP。 若要检查是否已取消 IRP，更高级别的驱动程序必须调用**IoSetCompletionRoutine**与*InvokeOnCancel*参数设置为**TRUE**然后才传递IRP 到下一个较低的驱动程序。 请参阅[完成 Irp](completing-irps.md)有关完成例程的详细信息。

更高级别的驱动程序不能调用**IoCancelIrp**与未分配的 IRP。

 

 




