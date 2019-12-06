---
title: 报告设备故障
description: 报告设备故障
ms.assetid: ca536547-d51a-4450-8a83-19aac67aab92
keywords:
- PnP WDK KMDF，设备故障
- 即插即用 WDK KMDF，设备故障
- 设备故障 WDK KMDF
- 故障设备 WDK KMDF
- WdfDeviceFailedAttemptRestart
- WdfDeviceFailedNoRestart
- 报告设备故障 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52319a0abeb81d9f66e0ef92faf4ef00d4c2b60b
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2019
ms.locfileid: "74863099"
---
# <a name="reporting-device-failures"></a>报告设备故障


有三种方法可以报告设备故障：

-  从[设备对象回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/#device-callbacks)返回时，驱动程序可以提供一个返回值，其[NT\_SUCCESS](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)（*状态*）等于**FALSE**。

-  驱动程序可以调用[**WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)。

-  在从其[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调例程返回时，函数驱动程序可以提供一个返回值，其[NT\_SUCCESS](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)（*状态*）等于**FALSE**。 如果安装为[筛选器]( https://docs.microsoft.com/windows-hardware/drivers/install/installing-a-filter-driver)的驱动程序未能[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)，则操作系统将跳过筛选器设备对象，而不表示 PnP 错误。

上述每种方法都会使框架有效地删除设备。 如果设备的驱动程序不支持系统上的其他设备，则 i/o 管理器将卸载驱动程序。

如果驱动程序的设备对象回调函数返回 NT\_SUCCESS （*状态*）等于**FALSE**的值，则该框架将通知 PnP 管理器，然后通过请求总线驱动程序 reenumerate 其设备来尝试重新启动设备。 如果卸载了驱动程序，将重新加载该驱动程序。

如果驱动程序调用[**WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)，则它会提供一个输入参数，该参数确定是否将重新启动设备。 参数值为**WdfDeviceFailedAttemptRestart**和**WdfDeviceFailedNoRestart**。

**UMDF**在 UMDF 2.15 之前，UMDF 驱动程序必须将此值设置为**WdfDeviceFailedNoRestart**。 从 UMDF 版本2.15 开始，UMDF 驱动程序可以通过调用[**WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed) ，并将*FailedAction*设置为**WdfDeviceFailedAttemptRestart**，请求基础总线驱动程序重新枚举该驱动程序。 有关详细信息，请参阅[**WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)。 

有关这些参数值的详细信息，请参阅[**WDF\_DEVICE\_FAILED\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_device_failed_action)。
在驱动程序的设备对象回调函数返回的值为其 NT\_SUCCESS （*状态*）等于**FALSE**的情况下，回调函数可以通过使用**WdfDeviceFailedNoRestart**的输入参数调用[**WdfDeviceSetFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetfailed)来阻止重新启动。 否则，这些回调函数不必调用**WdfDeviceSetFailed**。

如果在短时间内，多次连续的重新启动尝试会失败（因为重新启动的驱动程序再次报告错误），框架将停止尝试重新启动设备。

如果总线驱动程序的[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)函数返回一个值，而 NT\_SUCCESS （*状态*）等于**FALSE**，则该框架可能仍会调用与总线驱动程序的子设备关联的驱动程序的*EvtDeviceD0Entry*函数。

 

 





