---
title: 在 WBDI 驱动程序中使用 WinUSB
description: 在 WBDI 驱动程序中使用 WinUSB
ms.assetid: a2f109cd-cb61-4c63-8e93-111f62a2c02d
keywords:
- 生物识别驱动程序 WDK WinUSB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9008446f982d3bfc80ba40f16c8c9915524456c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575295"
---
# <a name="using-winusb-in-a-wbdi-driver"></a>在 WBDI 驱动程序中使用 WinUSB


Microsoft 建议 WBDI 驱动程序使用[USB I/O 目标](https://msdn.microsoft.com/library/windows/hardware/ff561358)生成到用户模式驱动程序框架 (UMDF)。

### <a name="span-idsettingumdfdispatcherspanspan-idsettingumdfdispatcherspansetting-umdfdispatcher"></a><span id="setting_umdfdispatcher"></span><span id="SETTING_UMDFDISPATCHER"></span>设置 UmdfDispatcher

安装了 UMDF 驱动程序的 INF 文件必须包含 WDF 特定**DDInstall**部分。 如果在 UMDF 中使用 USB I/O 目标，则必须设置在此 UmdfDispatcher 注册表指令**DDInstall**部分。

从 WudfBioUsbSample.inx 中下的一节[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)示例演示如何设置此指令：

```cpp
[Biometric_Install.NT.Wdf]
KmdfService=WINUSB, WinUsb_Install
UmdfDispatcher=WinUsb
UmdfService=WudfBioUsbSample, WudfBioUsbSample_Install
UmdfServiceOrder=WudfBioUsbSample
```

有关 UmdfDispatcher 的特定信息，请参阅[指定 UmdfDispatcher INF 指令](https://msdn.microsoft.com/library/windows/hardware/ff560526)。 WDF 注册表指令的常规信息，请参阅[指定 WDF 指令](https://msdn.microsoft.com/library/windows/hardware/ff560526)。

### <a name="span-idpendingasynchronousreadrequestsspanspan-idpendingasynchronousreadrequestsspanpending-asynchronous-read-requests"></a><span id="pending_asynchronous_read_requests"></span><span id="PENDING_ASYNCHRONOUS_READ_REQUESTS"></span>挂起的异步读取请求

WinUsb 可以处理多个未完成的读取的请求。 需要扫描期间的读取操作之间的最小延迟的设备应该保留一定数量的处理挂起的异步读取请求。 如果该驱动程序发出异步请求，WinUsb 发出这些请求在传输之前返回到完成例程的更早的读取请求的用户模式。

您可以参考`CBiometricDevice::InitiatePendingRead`方法中在 Device.cpp [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)若要查看挂起的读取请求方法的代码示例。

挂起的读取请求的代码应为循环的以下步骤：

1.  通过调用创建的预分配的 framework 内存对象[ **IWDFDriver::CreatePreallocatedWdfMemory**](https://msdn.microsoft.com/library/windows/hardware/ff558902)。

2.  提供的代码回调[ **OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)例程。 请参阅`CBiometricDevice::OnCompletion`示例中。

3.  获取一个指向[ **IRequestCallbackRequestCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556904)所属对象的接口。

4.  通过调用注册的回调函数[ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)并传入到指针[ **IRequestCallbackRequestCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff556904)在上一步中获得的。 I/O 请求完成时，框架将立即调用回调。

5.  调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)将读取的请求发送到设备。

6.  回调完成时，进程将读取请求。 之前[ **OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)例程启动新的挂起的读取请求，它应该检查 I/O 目标的状态。 若要执行此操作，查询[IWDFUsbTargetPipe](https://msdn.microsoft.com/library/windows/hardware/ff560391)指向的指针为其[IWDFIoTargetStateManagement](https://msdn.microsoft.com/library/windows/hardware/ff559198)接口。 然后调用[ **IWDFIoTargetStateManagement::GetState**](https://msdn.microsoft.com/library/windows/hardware/ff559202):
    ```cpp
    IWDFIoTarget * pTarget
    IWDFIoTargetStateManagement * pStateMgmt = NULL;
    WDF_IO_TARGET_STATE state;

    HRESULT hrQI = pTarget->QueryInterface(IID_PPV_ARGS(&pStateMgmt));
    WUDF_TEST_DRIVER_ASSERT((SUCCEEDED(hrQI) && pStateMgmt));

    state = pStateMgmt->GetState();
    ```

扫描完成后，取消任何挂起的读取请求。

如果您使用 UMDF USB 目标，则可以允许保持挂起状态的读取的请求跨电源关闭和强化。

如果不使用 UMDF USB 目标，该驱动程序应停止发送在 D0Exit 读取请求挂起并 D0Entry 在重新启动。

### <a name="span-idselectivesuspendspanspan-idselectivesuspendspanselective-suspend"></a><span id="selective_suspend"></span><span id="SELECTIVE_SUSPEND"></span>选择性挂起

WBDI 驱动程序应支持[USB 选择性挂起](../usbcon/usb-selective-suspend.md)。

支持系统项的设备和设备空闲应启用的注册表设置选择性挂起 WinUsb，在此代码示例摘自 WudfBioUsbSample.inx 中所示：

```cpp
HKR,,"SystemWakeEnabled",0x00010001,1
HKR,,"DeviceIdleEnabled",0x00010001,1
```

操作系统 USB 堆栈不能保证系统唤醒和驱动程序何时从设备开始读取之间的时间。

理想情况下，设备应处于状态准备就绪可捕获一次扫描时，系统挂起。 如果扫描发生在系统被挂起时，设备应缓存整个指纹扫描的输入的数据。 当系统被唤醒，驱动程序，然后读取中设备的数据。 通过支持这种情况下，您可以启用系统唤醒并解锁/登录方案。

 

 





