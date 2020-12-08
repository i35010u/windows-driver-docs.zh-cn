---
title: 在 WBDI 驱动程序中管理队列
description: 在 WBDI 驱动程序中管理队列
keywords:
- 生物识别驱动程序 WDK，管理队列
- 管理队列-WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6a44a4aaa77558d6fb4dcd94db7af7ac4009b12
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798623"
---
# <a name="managing-queues-in-a-wbdi-driver"></a>在 WBDI 驱动程序中管理队列


WBDI 驱动程序应创建至少一个队列来处理来自服务的多个并发请求。 如果使用的是 UMDF，可以利用其队列管理支持。

在 [WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)中，CBiometricIoQueue 类实现 i/o 队列接口。

`CBiometricIoQueue::Initialize`具体而言，驱动程序将查询所属的 CBiometricIoQueue 对象，以获取指向[IQueueCallbackDeviceIoControl](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)接口的指针，框架使用该接口来确定驱动程序在队列上订阅的事件回调函数：

```cpp
if (SUCCEEDED(hr)) 
{
hr = this->QueryInterface(__uuidof(IUnknown), (void **)&unknown);
}
```

然后，该驱动程序将调用 [**IWDFDevice：： CreateIoQueue**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue) 来配置默认 i/o 队列：

```cpp
hr = FxDevice->CreateIoQueue(unknown,
FALSE,
WdfIoQueueDispatchParallel,
FALSE,
FALSE,
&fxQueue);
BiometricSafeRelease(unknown);
```

调用指定 WdfIoQueueDispatchParallel，以便在请求可用时，框架会立即向驱动程序的 i/o 队列回调函数发出请求。

接下来，驱动程序调用 [**IWDFDevice：： ConfigureRequestDispatching**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-configurerequestdispatching) 来配置队列，以筛选所有设备 i/o 请求：

```cpp
hr = FxDevice->ConfigureRequestDispatching(fxQueue,
WdfRequestDeviceIoControl,
TRUE);
```

由于驱动程序在此调用中指定 WdfRequestDeviceIoControl，因此它提供了 [**OnDeviceIoControl**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol) 处理程序来处理来自框架的 i/o 通知。 它在 **IQueueCallbackDeviceIoControl：： OnDeviceIoControl** 方法中执行此操作，该方法是之前对 CreateIoQueue 的调用中 "unknown" 参数的一部分。

一次只能有一个未完成的 [**IOCTL \_ 生物识别 \_ 捕获 \_ 数据**](/windows-hardware/drivers/ddi/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_capture_data) 请求。 驱动程序应跟踪 IOCTL \_ 生物识别 \_ 捕获 \_ 数据请求，方法是将指针保存到挂起的请求或使用另一个框架队列处理这些请求。

在此示例中，如果有挂起的 i/o 请求，示例将在 CBiometricDevice 类的成员中维护一个指向请求的指针，如在设备 .h 中所定义：

```cpp
IWDFIoRequest *m_PendingRequest;
```

当一个传感器数据收集 i/o 处于挂起状态时，对数据收集 IOCTLs 的后续调用应该会失败：

```cpp
FxRequest->Complete(WINBIO_E_DATA_COLLECTION_IN_PROGRESS);
```

在完成或取消捕获请求时，此值设置为 **NULL**：

```cpp
IWDFIoRequest *FxRequest = (IWDFIoRequest *)InterlockedExchangePointer((PVOID *)&m_PendingRequest, NULL);
```

 

