---
title: 创建和使用驱动程序创建的文件对象
description: 创建和使用驱动程序创建的文件对象
ms.assetid: 84b677b4-fddf-4f06-9ea6-e4642c3f1b2d
keywords:
- 驱动程序创建的文件对象 WDK UMDF
- 驱动程序创建的文件对象 WDK UMDF，创建和使用
- 用于处理 i/o WDK UMDF、驱动程序创建、创建和使用的文件对象
- I/o 请求 WDK UMDF、file 对象、创建和使用
- 用户模式驱动程序框架 WDK，处理 i/o 的文件对象，创建和使用
- UMDF WDK，处理 i/o 的文件对象，创建和使用
- 用户模式驱动程序 WDK UMDF，处理 i/o 的文件对象，创建和使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5f2534fe60a6ce7d9137986a8e4ee1c2733d0e4
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210227"
---
# <a name="creating-and-using-driver-created-file-objects"></a>创建和使用驱动程序创建的文件对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

如果驱动程序需要创建独立于应用程序的 i/o 请求并将其发送到堆栈中的下一个驱动程序（默认 i/o 目标），则驱动程序必须创建并关闭其自己的文件对象。

### <a name="creating-a-file-object"></a>创建文件对象

驱动程序必须调用[**IWDFDevice：： CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)方法来创建用于驱动程序的文件对象。 当驱动程序调用**IWDFDevice：： CreateWdfFile**时，框架会将 create 请求发送到堆栈中的下一个驱动程序。 堆栈中的下一个驱动程序可能处于内核模式或用户模式下。

此创建文件请求处理在 Windows 驱动模型（WDM）中是不同的。 在 WDM 中，对[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)函数的调用会导致 create IRP 转向内核模式堆栈的顶部。 下图显示了在 UMDF 与 WDM 中创建文件请求的处理：

![在 umdf 与 wdm 中创建文件请求处理](images/drvrcrtfile.gif)

通过调用[**IWDFDevice：： CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)，驱动程序可以在启动整个堆栈之前，创建文件对象，然后在设备启动过程中发送 i/o 请求。

堆栈中的下一个驱动程序必须确定它是否可以处理创建文件请求，或者是否必须在堆栈中进一步转发请求。

调用[**IWDFDevice：： CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)之后，驱动程序无法取消创建操作。

## <a name="using-the-file-object"></a>使用 File 对象


若要将异步读取请求发送到其下堆叠的下一个驱动程序，你的驱动程序可以使用以下模式。

1.  调用[**IWDFDevice：： CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)以创建文件对象。
2.  调用[**IWDFDevice：： GetDefaultIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-getdefaultiotarget)以检索表示低级驱动程序的接口。
3.  调用[**IWDFDevice：： CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)以创建未格式化的[**IWDFIoRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)对象。
4.  调用[**IWDFIoRequest：： SetCompletionCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)来注册一个[**IRequestCallbackRequestCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)接口，该接口用于框架在 i/o 请求完成时调用的[**OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)方法。
5.  调用[**IWDFIoTarget：： FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)，在 *.pfile*参数中提供指向[**IWDFDriverCreatedFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdrivercreatedfile)接口的指针。
6.  调用[**IWDFIoRequest：： send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)发送请求。

## <a name="closing-the-file-object"></a>关闭文件对象


调用[**IWDFDevice：： CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)的驱动程序稍后必须调用[**IWDFDriverCreatedFile：： Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)。

通常，驱动程序从其[**IPnpCallbackHardware：： OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)或[**IPnpCallbackSelfManagedIo：： OnSelfManagedIoCleanup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediocleanup)回调方法中调用[**IWDFDriverCreatedFile：： Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close) 。

当驱动程序调用[**IWDFDriverCreatedFile：： Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)时，框架将调用下一个驱动程序的[**IFileCallbackCleanup：： OnCleanupFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)方法。 在此方法中，下一个驱动程序必须取消或完成与该文件对象关联的所有挂起的 i/o 请求。 然后，框架会取消由驱动程序创建的、名为[**IWDFDevice：： CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)的所有 i/o 请求。 框架不取消堆栈中较低的驱动程序可能与 file 对象相关联的任何 i/o 请求。 驱动程序负责取消所有此类请求。 仅当与该对象关联的所有 i/o 请求都完成后，该文件对象才会关闭。

接下来，该框架将调用下一个驱动程序的[**IFileCallbackClose：： OnCloseFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)方法。 此时，框架保证下一个驱动程序不会收到此文件对象的其他 i/o 请求。

在框架调用[**OnCloseFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)后，它会销毁表示 file 对象的[IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)接口。

如果在驱动程序的设备删除方法（例如[**IPnpCallbackHardware：： OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)和[**IPnpCallbackSelfManagedIo：： OnSelfManagedIoCleanup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediocleanup)）返回之后，驱动程序创建的文件对象仍然存在，则框架将生成驱动程序停止。 有关解决此问题的信息，请参阅[确定 UMDF 在设备删除时指示未完成文件的原因](determining-why-umdf-indicates-outstanding-files-at-device-removal-tim.md)。

 

 





