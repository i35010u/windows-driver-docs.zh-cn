---
title: 创建和使用驱动程序创建文件对象
description: 创建和使用驱动程序创建文件对象
ms.assetid: 84b677b4-fddf-4f06-9ea6-e4642c3f1b2d
keywords:
- 驱动程序创建文件对象 WDK UMDF
- 驱动程序创建文件对象 WDK UMDF，创建和使用
- 文件句柄 I/O WDK UMDF 驱动程序创建、 创建和使用的对象
- I/O 请求 WDK UMDF，文件对象，创建和使用
- 用户模式驱动程序框架 WDK、 I/O、 创建和使用句柄的文件对象
- UMDF WDK、 I/O、 创建和使用句柄的文件对象
- 用户模式驱动程序 WDK UMDF，文件 I/O，创建和使用句柄的对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ca6e7a6e717d78b4c938b0fc056188874f40d59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555170"
---
# <a name="creating-and-using-driver-created-file-objects"></a>创建和使用驱动程序创建文件对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果您的驱动程序需要创建并发送到堆栈 （默认 I/O 目标） 中的下一步驱动程序应用程序无关的 I/O 请求，该驱动程序必须创建并关闭其自己的文件对象。

### <a name="creating-a-file-object"></a>创建文件对象

您的驱动程序必须调用[ **IWDFDevice::CreateWdfFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558828)方法创建的驱动程序使用的文件对象。 当驱动程序调用**IWDFDevice::CreateWdfFile**，框架将创建请求发送到堆栈中的下一步驱动程序。 在内核模式下或在用户模式下，可能是在堆栈中的下一步驱动程序。

此创建文件请求处理是在 Windows 驱动程序模型 (WDM) 不同。 在 WDM，调用[ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)函数会导致创建 IRP 转到内核模式堆栈的顶部。 下图显示与 WDM UMDF 中创建文件请求处理：

![在与 wdm umdf 中处理的创建文件请求](images/drvrcrtfile.gif)

通过调用[ **IWDFDevice::CreateWdfFile**](https://msdn.microsoft.com/library/windows/hardware/ff558828)，驱动程序可以创建文件对象并之前已开始整个堆栈，在设备启动期间发送的 I/O 请求。

在堆栈中的下一步驱动程序必须确定是否可处理创建文件请求，或者它必须进一步在堆栈的下层将请求转发。

在调用[ **IWDFDevice::CreateWdfFile**](https://msdn.microsoft.com/library/windows/hardware/ff558828)，驱动程序不能取消创建操作。

## <a name="using-the-file-object"></a>使用文件对象


若要发送到下一步的驱动程序的异步读取的请求堆积下面，您的驱动程序可以使用以下模式。

1.  调用[ **IWDFDevice::CreateWdfFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558828)创建文件对象。
2.  调用[ **IWDFDevice::GetDefaultIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff558831)来检索表示较低级别的驱动程序的接口。
3.  调用[ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)若要创建未格式化[ **IWDFIoRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff558985)对象。
4.  调用[ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)注册[ **IRequestCallbackRequestCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556904) 接口[**OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)框架在 I/O 请求完成时调用的方法。
5.  调用[ **IWDFIoTarget::FormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559233)，提供一个指向[ **IWDFDriverCreatedFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558895)中接口*pFile*参数。
6.  调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)将请求发送。

## <a name="closing-the-file-object"></a>关闭文件对象


调用的驱动程序[ **IWDFDevice::CreateWdfFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558828)必须更高版本调用[ **IWDFDriverCreatedFile::Close**](https://msdn.microsoft.com/library/windows/hardware/ff558897)。

通常情况下，您的驱动程序调用[ **IWDFDriverCreatedFile::Close** ](https://msdn.microsoft.com/library/windows/hardware/ff558897)从其[ **IPnpCallbackHardware::OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556768)或[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoCleanup** ](https://msdn.microsoft.com/library/windows/hardware/ff556780)回调方法。

当驱动程序调用[ **IWDFDriverCreatedFile::Close**](https://msdn.microsoft.com/library/windows/hardware/ff558897)，框架将调用下一步的驱动程序[ **IFileCallbackCleanup::OnCleanupFile** ](https://msdn.microsoft.com/library/windows/hardware/ff554905)方法。 在此方法下, 一步的驱动程序必须取消或完成与文件对象相关联的所有挂起的 I/O 请求。 Framework 然后取消创建名为的驱动程序的所有 I/O 请求[ **IWDFDevice::CreateWdfFile**](https://msdn.microsoft.com/library/windows/hardware/ff558828)。 框架不会取消任何堆栈中的低级驱动程序可能包含关联的文件对象使用的 I/O 请求。 它是驱动程序的责任取消任何此类请求。 文件对象仅与之关联的所有 I/O 请求都完成后将关闭。

接下来，框架将调用下一步的驱动程序[ **IFileCallbackClose::OnCloseFile** ](https://msdn.microsoft.com/library/windows/hardware/ff554910)方法。 此时，该框架可保证下一步的驱动程序将不会收到此文件对象的其他 I/O 请求。

框架将调用后[ **OnCloseFile**](https://msdn.microsoft.com/library/windows/hardware/ff554910)，它将销毁[IWDFFile](https://msdn.microsoft.com/library/windows/hardware/ff558912)表示文件对象的接口。

如果驱动程序的设备删除方法后保持驱动程序创建文件对象 (例如[ **IPnpCallbackHardware::OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556768)并[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoCleanup**](https://msdn.microsoft.com/library/windows/hardware/ff556780)) 返回，框架才生成驱动程序停止。 有关此问题的疑难解答信息，请参阅[确定为什么 UMDF 指示未完成的文件在设备删除时](determining-why-umdf-indicates-outstanding-files-at-device-removal-tim.md)。

 

 





