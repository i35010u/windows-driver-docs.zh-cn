---
title: 支持生物识别 IOCTL 调用序列
description: 支持生物识别 IOCTL 调用序列
ms.assetid: e6555895-8936-4f5d-8f2b-05b5283edbee
keywords:
- 生物识别驱动程序 WDK，支持 IOCTLs
- 支持 IOCTLs WDK 生物识别
- IOCTLs WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49719c03fd32e24fab86c46d0fa8ced51bf327d3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832214"
---
# <a name="supporting-biometric-ioctl-calling-sequence"></a>支持生物识别 IOCTL 调用序列


WBDI 是基于 Windows 标准 IOCTL 的接口。 编写 WBDI 驱动程序时，必须支持一组必需的 IOCTLs。 你还可以选择支持可选的 IOCTLs。 可以在[生物识别 IOCTLs](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)中找到必需和可选 IOCTLs 的完整列表。

供应商提供的 WBDI 驱动程序应准备好从 Windows 生物识别服务（WBS）按以下顺序接收 IOCTL 请求。 可以在[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)的 IOCTLs 中查看这些的处理程序示例。

1.  Windows 生物识别服务或传感器适配器初始化生物识别设备，并验证该设备是否可供使用。 服务或适配器发送[**IOCTL\_生物识别\_获取\_的属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_attributes)请求。

    驱动程序接收指向[**WINBIO\_传感器\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_sensor_attributes)结构的指针。 在此 IOCTL 的处理程序中，驱动程序应填写此结构的相关成员，并通过调用[**IWDFIoRequest：： complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)来完成请求。

2.  接下来，驱动程序接收[**IOCTL\_生物识别\_获取\_传感器\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_sensor_status)。 驱动程序应填写[**WINBIO\_诊断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics)结构的相关成员并完成该请求。

3.  如果驱动程序指示在 IOCTL\_生物识别\_获取\_传感器\_状态请求的**SensorStatus** [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics)成员中需要校准，则接下来，驱动程序将接收[**IOCTL\_生物识别\_校准**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_calibrate)请求。 驱动程序必须为此 IOCTL 提供处理程序。 校准设备后，回调应返回[**WINBIO\_校准\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_calibration_info)结构。

4.  现在，驱动程序可以接收[**IOCTL\_生物识别\_捕获\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_capture_data)请求。 由于任何时候都只能挂起一个捕获，因此此请求的处理程序应该首先确认没有任何请求处于挂起状态。 如果请求处于挂起状态，则在\_进度下，使用 WINBIO\_E\_数据\_集合\_来完成请求。

    WinBio 服务或应用程序可以通过调用 Win32 取消例程（如[**CancelIo**](https://docs.microsoft.com/windows/desktop/FileIO/cancelio)、 [**CancelIoEx**](https://docs.microsoft.com/windows/desktop/FileIO/cancelioex-func)或[**CancelSynchronousIo**](https://docs.microsoft.com/windows/desktop/FileIO/cancelsynchronousio-func)）来请求取消未完成的捕获请求。 同样，WBDI 驱动程序也必须支持取消操作。

    驱动程序通过调用[**IWDFIoRequest：： MarkCancelable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-markcancelable)来注册[IRequestCallbackCancel](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackcancel)接口来处理取消操作。

    然后，处理程序将设备计划为捕获模式并从回调返回。 请求应始终处于挂起状态，直到被取消或驱动程序检测到捕获完成。 此 i/o 请求完成后，设备可返回到空闲状态。 客户端可以对 IOCTL\_生物首次调用\_捕获\_数据，以确定实际捕获的正确缓冲区大小。

5.  用于[**IOCTL\_生物识别**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_reset)的处理程序\_RESET 应以物理方式将设备重置为已知或空闲状态。 此请求的处理程序还必须取消任何挂起的数据收集 i/o，并填写[**WINBIO\_空白\_负载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_blank_payload)结构。 然后，处理程序完成请求。 客户端不需要在对 IOCTL\_生物识别调用之间调用 reset\_捕获\_数据。

 

 





