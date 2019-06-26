---
title: 在 WBDI 驱动程序中管理队列
description: 在 WBDI 驱动程序中管理队列
ms.assetid: f0434581-8492-42e1-ae50-4114e7b8b202
keywords:
- 生物识别驱动程序 WDK、 管理队列
- 管理队列 WDK 生物识别
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37351b27d8ca02c4def553b19131f09425ce6b60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364689"
---
# <a name="managing-queues-in-a-wbdi-driver"></a>在 WBDI 驱动程序中管理队列


WBDI 驱动程序应创建至少一个队列来处理来自服务的多个并发请求。 如果使用 UMDF，您可以利用其队列管理支持。

在中[WudfBioUsbSample](https://github.com/Microsoft/Windows-driver-samples/tree/master/biometrics/driver)，CBiometricIoQueue 类实现的 I/O 队列接口。

在方法中`CBiometricIoQueue::Initialize`，具体而言，驱动程序将查询指向的所属 CBiometricIoQueue 对象[IQueueCallbackDeviceIoControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)框架使用以确定事件回调函数的接口该驱动程序订阅的队列：

```cpp
if (SUCCEEDED(hr)) 
{
hr = this->QueryInterface(__uuidof(IUnknown), (void **)&unknown);
}
```

然后驱动程序调用[ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)若要配置默认的 I/O 队列：

```cpp
hr = FxDevice->CreateIoQueue(unknown,
FALSE,
WdfIoQueueDispatchParallel,
FALSE,
FALSE,
&fxQueue);
BiometricSafeRelease(unknown);
```

调用指定 WdfIoQueueDispatchParallel，以便个请求均可用后，框架将显示对驱动程序的 I/O 队列回调函数的请求。

接下来，驱动程序调用[ **IWDFDevice::ConfigureRequestDispatching** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-configurerequestdispatching)来配置要筛选的所有设备 I/O 请求的队列：

```cpp
hr = FxDevice->ConfigureRequestDispatching(fxQueue,
WdfRequestDeviceIoControl,
TRUE);
```

由于该驱动程序在此调用中指定 WdfRequestDeviceIoControl，它提供了[ **OnDeviceIoControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)进程 I/O 通知框架中的处理程序。 此**IQueueCallbackDeviceIoControl::OnDeviceIoControl**以前是到 CreateIoQueue 调用中的"未知"参数的一部分的方法。

只能有一个未完成[ **IOCTL\_生物识别\_捕获\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winbio_ioctl/ni-winbio_ioctl-ioctl_biometric_capture_data)请求一次。 该驱动程序应在跟踪 IOCTL\_生物识别\_捕获\_数据请求，通过在内部保持挂起的请求一个指针，或通过使用另一个框架队列来处理这些请求。

在示例中，如果存在挂起的 I/O 请求，该示例维护一个指向 CBiometricDevice 类的成员中的请求中 Device.h 定义：

```cpp
IWDFIoRequest *m_PendingRequest;
```

一个传感器数据收集 I/O 挂起时，数据收集到的后续调用应失败 Ioctl:

```cpp
FxRequest->Complete(WINBIO_E_DATA_COLLECTION_IN_PROGRESS);
```

当捕获请求是已完成或取消时，此值设置为**NULL**:

```cpp
IWDFIoRequest *FxRequest = (IWDFIoRequest *)InterlockedExchangePointer((PVOID *)&m_PendingRequest, NULL);
```

 

 





