---
title: 创建中断对象
description: 创建中断对象
ms.assetid: 8bea7498-9fee-4d84-9e6b-976102c54876
keywords:
- 硬件中断 WDK KMDF，对象创建
- 中断 WDK KMDF，对象创建
- 消息信号中断 WDK KMDF
- Msi WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5466e4b38f4c6ca08318e572eb2b7cb856a33143
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358479"
---
# <a name="creating-an-interrupt-object"></a>创建中断对象


处理设备的硬件中断的 Windows 驱动程序框架 (WDF) 驱动程序必须创建每个设备可以支持每个中断 framework 中断对象。 内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序可以在 framework 版本 1.11 更高版本上并正在运行 Windows 8 或更高版本的操作系统中，创建需要的中断对象[被动级别处理](supporting-passive-level-interrupts.md). 除非芯片 (SoC) 平台上，要为系统编写驱动程序，但是，您的驱动程序应使用 DIRQL 中断对象。

驱动程序通常创建框架中的中断对象及其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。 驱动程序还可以创建中断对象从其[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调函数。

框架将调用的驱动程序[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数之前插即用 (PnP) 管理器已分配给设备的系统资源，例如中断向量。 PnP 管理器中向资源分配后，框架将中断资源存储在设备的中断对象。 (驱动程序的[不支持即插](using-kernel-mode-driver-framework-with-non-pnp-drivers.md)不能使用中断对象。)

若要创建 framework 中断对象，您的驱动程序必须初始化[ **WDF\_中断\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552347)结构并将其传递给[ **WdfInterruptCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547345)方法。

UMDF 支持以下类型的中断：

-   级别触发 （共享或排他）
-   边缘触发 （不包括仅）
-   MSI （不含定义）

**请注意**  UMDF 不支持*共享*边缘触发中断。

 

从 UMDF 2.15 版本开始，则 UMDF 支持的硬件按钮，您不能启用或禁用显式使用硬件寄存器通常由 GPIO 插针之类的简单设备中断。 若要支持此类设备，UMDF 驱动程序必须使用独占边缘触发中断。

从开始 KMDF 版本 1.15，KMDF 还支持中断对于此类设备，没有解决方法中所述[处理 Active-Both 中断](handling-active-both-interrupts.md)。

另外，请在[ **WDF\_中断\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff552347)，您的驱动程序提供以下驱动程序所提供事件回调函数的指针：

<a href="" id="---------evtinterruptenable--------"></a>[*EvtInterruptEnable*](https://msdn.microsoft.com/library/windows/hardware/ff541730)  
启用的硬件中断。

<a href="" id="---------evtinterruptdisable--------"></a>[*EvtInterruptDisable*](https://msdn.microsoft.com/library/windows/hardware/ff541714)  
禁用的硬件中断。

<a href="" id="---------evtinterruptisr--------"></a>[*EvtInterruptIsr*](https://msdn.microsoft.com/library/windows/hardware/ff541735)  
中断中断服务的例程 (ISR)。

<a href="" id="---------evtinterruptdpc--------"></a>[*EvtInterruptDpc*](https://msdn.microsoft.com/library/windows/hardware/ff541721)  
延迟过程调用 (DPC) 的中断。

<a href="" id="evtinterruptworkitem"></a>[*EvtInterruptWorkItem*](https://msdn.microsoft.com/library/windows/hardware/hh406422)  
有关工作项[被动级别中断](supporting-passive-level-interrupts.md)。

有关使用框架版本 1.11 或更高版本在 Windows 8 或更高版本的操作系统的驱动程序，该驱动程序可以 framework 中断对象 （DIRQL 或被动） 的父对象显式设置为 framework 设备对象或 framework 队列对象。 如果该驱动程序指定一个父级，该驱动程序必须设置**AutomaticSerialization**中断对象的成员[ **WDF\_中断\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552347)为 TRUE 的结构。 (回想一下，如果**AutomaticSerialization**为 TRUE，框架将同步执行的中断对象[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)或[ *EvtInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh406422)从中断的父对象下的其他对象的回调函数的回调函数。)

例如，驱动程序可能作为父级的中断，若要将队列的回调与中断的同步指定队列[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)或[ *EvtInterruptWorkItem* ](https://msdn.microsoft.com/library/windows/hardware/hh406422)回调。 在此配置中，框架将删除的设备对象时删除队列对象。

在调用[ **WdfInterruptCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547345)，该驱动程序可以选择调用[ **WdfInterruptSetPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff547387)或[ **WdfInterruptSetExtendedPolicy** ](https://msdn.microsoft.com/library/windows/hardware/ff547381)若要指定其他中断参数。 通常，驱动程序会调用这些方法从其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。

框架将自动删除之前删除中断的父级的中断。 （可选） 一个驱动程序可以调用[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)若要删除在较早的时间的中断。

## <a name="supporting-message-signaled-interrupts"></a>支持消息信号中断


从 Windows Vista 开始支持消息信号中断 (Msi)。 若要启用操作系统可以支持你的设备中的 Msi，驱动程序的 INF 文件必须在注册表中设置一些值。 有关如何设置这些值的信息，请参阅[Enabling Message-Signaled 中断在注册表中](https://msdn.microsoft.com/library/windows/hardware/ff544246)。

您的驱动程序应创建为每个中断矢量或 MSI 消息，设备可以支持的框架中断对象。 如果 PnP 管理器不会授予设备的所有设备可以支持中断资源，不会使用额外的中断对象并不会调用它们的回调函数。

在 Windows 7 中，操作系统不支持资源请求的每个设备函数的多个 910 中断消息。 在 Windows 8 中，操作系统不支持资源请求为每个设备函数超过 2048 个中断。

如果设备驱动程序超出此限制，则设备可能无法启动。 若要运行包含多个逻辑处理器的计算机中，驱动程序不应请求每个处理器的多个中断。

驱动程序必须承受，正常情况下，重新平衡的系统中断资源在其中的即插即用的管理器将分配给设备的替代方法的任何组中断资源要求列表中的资源。 例如，设备可能会分配比请求的驱动程序较小数目的消息中断。 在最坏的情况下，驱动程序必须准备好运行只是一个基于行的中断的设备。

 

 





