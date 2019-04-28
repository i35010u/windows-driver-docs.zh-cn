---
title: 检测子设备
description: 检测子设备
ms.assetid: 36c0c4ef-7810-4e8a-b349-0b7c1f8c2f0c
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，子设备
- 子设备 WDK 微型端口，检测
- 检测子设备 WDK 微型端口
- HwVidGetVideoChildDescriptor
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e6978919b2dce9f3f36ca7c44f8735aa4626387
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348841"
---
# <a name="detecting-child-devices"></a>检测子设备


## <span id="ddk_detecting_child_devices_gg"></span><span id="DDK_DETECTING_CHILD_DEVICES_GG"></span>


必须实现[ *HwVidGetVideoChildDescriptor* ](https://msdn.microsoft.com/library/windows/hardware/ff567341)插管理器能够检测到的图形适配器的子设备微型端口驱动程序中。

默认情况下[ *HwVidGetVideoChildDescriptor* ](https://msdn.microsoft.com/library/windows/hardware/ff567341)后父设备是否已启动; 不能调用之前，即*HwVidGetVideoChildDescriptor*不能调用直到后[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)已完成。 若要替代此默认设置，从而允许子枚举发生在任何时候，可以设置**AllowEarlyEnumeration**的成员[**视频\_HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff570505)到**TRUE**。

当新的硬件连接到系统或现有的硬件系统断开连接时，某些设备生成中断。 若要处理此类中断，微型端口驱动程序应执行以下操作：

-   实现 DPC ([**HwVidDpcRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff567327)) 来调用[ **VideoPortEnumerateChildren**](https://msdn.microsoft.com/library/windows/hardware/ff570297)。

-   实现一个中断处理程序 ([*HwVidInterrupt*](https://msdn.microsoft.com/library/windows/hardware/ff567349)) 来调用[ **VideoPortQueueDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff570339)进行排队时在中断 DPC设备会发生。

[**VideoPortEnumerateChildren** ](https://msdn.microsoft.com/library/windows/hardware/ff570297)微型端口驱动程序，从而强制的适配器的子设备重新枚举[ *HwVidGetVideoChildDescriptor* ](https://msdn.microsoft.com/library/windows/hardware/ff567341)函数若要调用的每个父设备的子级。 插管理器将相应地更新父设备与其子项之间的关系。

 

 





