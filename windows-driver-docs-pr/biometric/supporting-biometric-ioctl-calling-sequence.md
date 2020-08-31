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
ms.openlocfilehash: 66725341fe4717fb1ff89f1212f3f2a8bd19a9d5
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095409"
---
# <a name="supporting-biometric-ioctl-calling-sequence"></a>支持生物识别 IOCTL 调用序列


WBDI 是基于 Windows 标准 IOCTL 的接口。 编写 WBDI 驱动程序时，必须支持一组必需的 IOCTLs。 你还可以选择支持可选的 IOCTLs。 可以在 [生物识别 IOCTLs](/windows-hardware/drivers/ddi/index)中找到必需和可选 IOCTLs 的完整列表。

供应商提供的 WBDI 驱动程序应准备好按以下顺序从 Windows 生物识别服务 (WBS) 接收 IOCTL 请求。 可以在 [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)的 IOCTLs 中查看这些的处理程序示例。

1.  Windows 生物识别服务或传感器适配器初始化生物识别设备，并验证该设备是否可供使用。 服务或适配器发送 [**IOCTL \_ 生物识别请求 \_ \_ 属性**](/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_attributes) 请求。

    驱动程序收到指向 [**WINBIO \_ 传感器 \_ 属性**](/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_sensor_attributes) 结构的指针。 在此 IOCTL 的处理程序中，驱动程序应填写此结构的相关成员，并通过调用 [**IWDFIoRequest：： complete**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)来完成请求。

2.  接下来，驱动程序接收 [**IOCTL \_ 生物识别 \_ \_ 传感器 \_ 状态**](/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_get_sensor_status)。 驱动程序应填写 [**WINBIO \_ 诊断**](/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics) 结构的相关成员并完成该请求。

3.  如果驱动程序指示在从 IOCTL 生物识别获取传感器状态请求中返回的[**WINBIO \_ 诊断**](/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_diagnostics)结构的**SensorStatus**成员中需要校准 \_ \_ \_ \_ ，则驱动程序接下来会接收[**ioctl \_ 生物识别 \_ 校准**](/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_calibrate)请求。 驱动程序必须为此 IOCTL 提供处理程序。 校准设备后，回调应返回 [**WINBIO \_ 校准 \_ 信息**](/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_calibration_info) 结构。

4.  现在，驱动程序可以接收 [**IOCTL \_ 生物识别 \_ 捕获 \_ 数据**](/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_capture_data) 请求。 由于任何时候都只能挂起一个捕获，因此此请求的处理程序应该首先确认没有任何请求处于挂起状态。 如果请求处于挂起状态，则完成包含 WINBIO \_ E 数据收集的请求 \_ \_ \_ \_ 。

    WinBio 服务或应用程序可以通过调用 Win32 取消例程（如 [**CancelIo**](/windows/desktop/FileIO/cancelio)、 [**CancelIoEx**](/windows/desktop/FileIO/cancelioex-func)或 [**CancelSynchronousIo**](/windows/desktop/FileIO/cancelsynchronousio-func)）来请求取消未完成的捕获请求。 同样，WBDI 驱动程序也必须支持取消操作。

    驱动程序通过调用 [**IWDFIoRequest：： MarkCancelable**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-markcancelable) 来注册 [IRequestCallbackCancel](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackcancel) 接口来处理取消操作。

    然后，处理程序将设备计划为捕获模式并从回调返回。 请求应始终处于挂起状态，直到被取消或驱动程序检测到捕获完成。 此 i/o 请求完成后，设备可返回到空闲状态。 客户端可以对 IOCTL \_ 生物识别捕获数据进行初始调用 \_ \_ ，以确定实际捕获的正确缓冲区大小。

5.  [**IOCTL \_ 生物识别 \_ 重置**](/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_reset)处理程序应以物理方式将设备重置为已知或空闲状态。 此请求的处理程序还必须取消任何挂起的数据收集 i/o，并填写 [**WINBIO \_ 空白 \_ 负载**](/windows-hardware/drivers/ddi/winbio_ioctl/ns-winbio_ioctl-_winbio_blank_payload) 结构。 然后，处理程序完成请求。 客户端不需要调用对 IOCTL \_ 生物识别捕获数据的调用之间的重置 \_ \_ 。

 

