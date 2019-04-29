---
title: 报告设备故障
description: 报告设备故障
ms.assetid: ca536547-d51a-4450-8a83-19aac67aab92
keywords:
- 即插即用 WDK KMDF，设备故障
- 插 WDK KMDF，设备故障
- 设备故障 WDK KMDF
- 失败的设备 WDK KMDF
- WdfDeviceFailedAttemptRestart
- WdfDeviceFailedNoRestart
- 报告设备失败 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a52d23061350a2e5009300467bffa17666c06068
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390034"
---
# <a name="reporting-device-failures"></a>报告设备故障


有两种方式可以报告设备失败：

-   从返回时[设备对象回叫函数](https://msdn.microsoft.com/library/windows/hardware/dn265631#device-callbacks)，该驱动程序可以为其提供一个返回值[NT\_成功](https://msdn.microsoft.com/library/windows/hardware/ff565436)(*状态*) 等于**FALSE**。

-   该驱动程序可以调用[ **WdfDeviceSetFailed**](https://msdn.microsoft.com/library/windows/hardware/ff546890)。

对于这两种方法，该框架有效地删除的设备。 如果设备的驱动程序在系统上不支持其他设备，I/O 管理器卸载驱动程序。

如果驱动程序的设备对象回叫函数返回的值的 NT\_成功 (*状态*) 等于**FALSE**，框架会通知即插即用管理器，然后尝试重新启动通过请求总线驱动程序 reenumerate 其设备的设备。 您的驱动程序将重新加载，如果它已被卸载。

如果您的驱动程序调用[ **WdfDeviceSetFailed**](https://msdn.microsoft.com/library/windows/hardware/ff546890)，它提供一个输入的参数，用于确定是否将重新启动设备。 此参数值为**WdfDeviceFailedAttemptRestart**并**WdfDeviceFailedNoRestart**。

**UMDF** UMDF 驱动程序必须将此值设置为**WdfDeviceFailedNoRestart**。

有关这些参数值的详细信息，请参阅[ **WDF\_设备\_失败\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff551253)。
之前驱动程序的设备对象的回调函数返回值的 NT\_成功 (*状态*) 等于**FALSE**，回调函数可以通过调用防止发生重新启动[ **WdfDeviceSetFailed** ](https://msdn.microsoft.com/library/windows/hardware/ff546890)带有输入参数**WdfDeviceFailedNoRestart**。 否则，这些回调函数不需要调用**WdfDeviceSetFailed**。

如果在短时间段内，多个连续的重新启动尝试失败 （因为重新启动的驱动程序再次报告错误），该框架将停止尝试重启设备。

如果总线驱动程序[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)函数返回的值的 NT\_成功 (*状态*) 等于**FALSE**仍可能调用框架*EvtDeviceD0Entry*与总线驱动程序的子设备关联的驱动程序的函数。

 

 





