---
title: 在 WBDI 驱动程序中使用 WinUSB
description: 在 WBDI 驱动程序中使用 WinUSB
ms.assetid: a2f109cd-cb61-4c63-8e93-111f62a2c02d
keywords:
- 生物识别驱动程序 WDK，WinUSB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db1906e4202fba1cd20f319fa51f5da2edb1c51c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833912"
---
# <a name="using-winusb-in-a-wbdi-driver"></a>在 WBDI 驱动程序中使用 WinUSB


Microsoft 建议 WBDI 驱动程序使用内置于用户模式驱动程序框架（UMDF）的[USB i/o 目标](https://docs.microsoft.com/windows-hardware/drivers/wdf/usb-i-o-targets-in-umdf)。

### <a name="span-idsetting_umdfdispatcherspanspan-idsetting_umdfdispatcherspansetting-umdfdispatcher"></a><span id="setting_umdfdispatcher"></span><span id="SETTING_UMDFDISPATCHER"></span>设置 UmdfDispatcher

安装 UMDF 驱动程序的 INF 文件必须包含 WDF 特定的**DDInstall**部分。 如果在 UMDF 中使用 USB i/o 目标，则必须在此**DDInstall**部分中设置 UmdfDispatcher 注册表指令。

[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)示例中的 WudfBioUsbSample inx 的以下部分演示如何设置此指令：

```cpp
[Biometric_Install.NT.Wdf]
KmdfService=WINUSB, WinUsb_Install
UmdfDispatcher=WinUsb
UmdfService=WudfBioUsbSample, WudfBioUsbSample_Install
UmdfServiceOrder=WudfBioUsbSample
```

有关 UmdfDispatcher 的特定信息，请参阅[指定 UMDFDISPATCHER INF 指令](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)。 有关 WDF 注册表指令的一般信息，请参阅[指定 Wdf 指令](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)。

### <a name="span-idpending_asynchronous_read_requestsspanspan-idpending_asynchronous_read_requestsspanpending-asynchronous-read-requests"></a><span id="pending_asynchronous_read_requests"></span><span id="PENDING_ASYNCHRONOUS_READ_REQUESTS"></span>挂起的异步读取请求

WinUsb 可以处理多个未处理的读取请求。 在扫描过程中，在读取操作期间要求最小延迟的设备应保留一些挂起的待处理异步读取请求。 如果驱动程序发出异步请求，WinUsb 会在传输回用户模式之前发出这些请求，以完成较早读取请求的完成例程。

可以在 WudfBioUsbSample 中的[](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)中引用 `CBiometricDevice::InitiatePendingRead` 方法，以查看有关如何挂起读取请求的代码示例。

挂起读取请求的代码应为以下步骤的循环：

1.  通过调用[**IWDFDriver：： CreatePreallocatedWdfMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createpreallocatedwdfmemory)创建预分配的框架内存对象。

2.  在[**OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)例程中提供回调代码。 请参阅示例中的 `CBiometricDevice::OnCompletion`。

3.  获取指向所属对象的[**IRequestCallbackRequestCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)接口的指针。

4.  通过调用[**IWDFIoRequest：： SetCompletionCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)注册回调函数，并将指针传入到在上一步中获得的[**IRequestCallbackRequestCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion) 。 现在，在 i/o 请求完成后，框架将调用回调。

5.  调用[**IWDFIoRequest：： send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)将读取请求发送到设备。

6.  完成回调后，处理读取请求。 在[**OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)例程启动新的挂起读取请求之前，它应检查 i/o 目标的状态。 为此，请查询[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)以获取指向其[IWDFIoTargetStateManagement](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)接口的指针。 然后调用[**IWDFIoTargetStateManagement：： GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-getstate)：
    ```cpp
    IWDFIoTarget * pTarget
    IWDFIoTargetStateManagement * pStateMgmt = NULL;
    WDF_IO_TARGET_STATE state;

    HRESULT hrQI = pTarget->QueryInterface(IID_PPV_ARGS(&pStateMgmt));
    WUDF_TEST_DRIVER_ASSERT((SUCCEEDED(hrQI) && pStateMgmt));

    state = pStateMgmt->GetState();
    ```

扫描完成后，取消任何挂起的读取请求。

如果你使用的是 UMDF USB 目标，则可以允许读取请求在关闭电源和通电后保持挂起状态。

如果不使用 UMDF-USB 目标，则驱动程序应停止在 D0Exit 发送挂起的读取请求，并在 D0Entry 上重新启动。

### <a name="span-idselective_suspendspanspan-idselective_suspendspanselective-suspend"></a><span id="selective_suspend"></span><span id="SELECTIVE_SUSPEND"></span>选择性挂起

WBDI 驱动程序应支持[USB 选择性挂起](../usbcon/usb-selective-suspend.md)。

支持系统唤醒和设备空闲的设备应在 WinUsb 中启用选择性挂起的注册表设置，如 WudfBioUsbSample. inx 中的此代码示例所示：

```cpp
HKR,,"SystemWakeEnabled",0x00010001,1
HKR,,"DeviceIdleEnabled",0x00010001,1
```

当驱动程序可以开始从设备读取时，操作系统 USB 堆栈无法保证系统唤醒之间的时间。

理想情况下，设备应处于 "就绪" 状态，以便在系统挂起时捕获扫描。 如果在系统挂起时进行扫描，则设备应缓存用于整个指纹扫描的输入数据。 当系统唤醒时，驱动程序将从设备读取数据。 通过支持此方案，可以启用系统唤醒和解锁/登录方案。

 

 





