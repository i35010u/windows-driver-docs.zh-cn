---
title: 创建一个中断对象
description: 创建一个中断对象
ms.assetid: D281F2E8-3ADA-4F4E-B345-CE72FA3C69EC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5304ab2e648dfcaa0c39f8a764ab2e1a41de6842
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523409"
---
# <a name="creating-an-interrupt-object"></a>创建一个中断对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

处理设备的硬件中断的 UMDF 驱动程序必须创建每个设备可以支持每个中断 framework 中断对象。

通常情况下，驱动程序创建框架中的中断对象[ **IDriverEntry::OnDeviceAdd**](https://msdn.microsoft.com/library/windows/hardware/ff554896)。 但是，还可以创建中的中断对象[ **IPnpCallbackHardware2::OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/hh439734)。

若要创建 framework 中断对象，您的驱动程序必须初始化[ **WUDF\_中断\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/hh464084)结构并将其传递给[ **IWDFDevice3::CreateInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451208)方法。 此方法将注册以下驱动程序所提供事件回调函数：

<a href="" id="oninterruptenable"></a>[*OnInterruptEnable*](https://msdn.microsoft.com/library/windows/hardware/hh463899)  
启用的硬件中断。

<a href="" id="oninterruptdisable"></a>[*OnInterruptDisable*](https://msdn.microsoft.com/library/windows/hardware/hh463895)  
禁用的硬件中断。

<a href="" id="oninterruptisr"></a>[*OnInterruptIsr*](https://msdn.microsoft.com/library/windows/hardware/hh463902)  
中断服务例程 (ISR) 中断。

<a href="" id="oninterruptworkitem"></a>[*OnInterruptWorkItem*](https://msdn.microsoft.com/library/windows/hardware/hh463905)  
中断工作人员例程。

（可选） 该驱动程序可以调用[ **IWDFInterrupt::SetPolicy** ](https://msdn.microsoft.com/library/windows/hardware/hh451328)或[ **IWDFInterrupt::SetExtendedPolicy** ](https://msdn.microsoft.com/library/windows/hardware/hh451324)若要指定其他中断参数。

框架将调用的驱动程序[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)回调函数之前插即用 (PnP) 管理器已分配给设备的系统资源，例如中断向量。 PnP 管理器中向资源分配后，框架将中断资源存储在设备的中断对象。 （不支持即插的驱动程序不能使用中断对象。）

在 Windows Vista 和更高版本的操作系统支持消息信号中断 (Msi)。 若要启用操作系统可以支持你的设备中的 Msi，驱动程序的 INF 文件必须在注册表中设置一些值。 有关如何设置这些值的信息，请参阅[Enabling Message-Signaled 中断在注册表中](https://msdn.microsoft.com/library/windows/hardware/ff544246)。

如果设备可以支持一定数量的 MSI 消息，即插即用管理器将尝试向设备分配该数目的消息。 如果 PnP 管理器不能分配的所有设备可以支持消息，它将向设备分配一个消息。

您的驱动程序应创建为每个中断矢量或 MSI 消息，设备可以支持的框架中断对象。 如果 PnP 管理器不会授予设备的所有设备可以支持中断资源，不会使用额外的中断对象，并且不会调用其回调函数。

 

 





