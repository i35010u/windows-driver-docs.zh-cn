---
title: 报告当系统回到 S0 状态时设备开机
description: 报告当系统回到 S0 状态时设备开机
ms.assetid: 35A48B37-8000-45DC-8E39-4B58ABE7DE68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 978d5244b51c6e40f571856142fc4abb5db930ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842221"
---
# <a name="reporting-device-powered-on-when-system-returns-to-s0"></a>报告当系统回到 S0 状态时设备开机


\[仅适用于 KMDF\]

当系统从低功耗状态返回到其工作（S0）状态时，PnP 管理器会将系统设置-power IRP （[**IRP\_MN\_集\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)）发送到设备，使其正常工作（D0）状态。 WDF 处理系统设置-power IRP。 但是，因为在多组件方案中，驱动程序已直接注册到电源管理框架（PoFx），所以当设备完成过渡到完全打开（D0）电源时，驱动程序必须调用[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)状态. 驱动程序可以通过在系统设置-power IRP 到达时注册一项 WDM 预处理例程来接收通知，来实现此目的。

驱动程序可以使用以下过程：

1.  调用[**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignwdmirppreprocesscallback) ，以便为[**IRP\_MN\_集\_幂**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)注册[*EvtDeviceWdmIrpPreprocess*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdfdevice_wdm_irp_preprocess)回调函数。 在回调中，驱动程序在其设备扩展中设置标志，以指示它需要从其下一个[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)回调调用[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon) 。
2.  在[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)中，如果设置了标志，驱动程序将清除标志并调用[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon)。
3.  驱动程序还会检查[*EvtDeviceSelfManagedIoFlush*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_self_managed_io_flush)中的标志。 如果设置了标志，则设备无法返回到 D0 并且设备已被删除。 在这种情况下，驱动程序调用[**PoFxReportDevicePoweredOn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pofxreportdevicepoweredon) ，然后将其与 power framework 一起取消注册。

 

 





