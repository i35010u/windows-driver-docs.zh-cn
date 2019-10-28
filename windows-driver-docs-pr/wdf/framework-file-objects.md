---
title: 框架文件对象
description: 框架文件对象
ms.assetid: 93ec5dd7-8ef0-4cea-9253-ea5d7869d4b8
keywords:
- I/o 请求 WDK KMDF，文件对象
- 文件对象 WDK KMDF
- 请求处理 WDK KMDF，文件对象
- framework 对象 WDK KMDF，文件对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e7946f9ddb7a2342aca791c6b7b8ea151b6b827
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843174"
---
# <a name="framework-file-objects"></a>框架文件对象





当应用程序或驱动程序尝试访问设备时（通常通过创建或打开文件），操作系统会将文件创建请求发送到驱动程序堆栈。 当应用程序或驱动程序使用完设备后，系统会将文件清理和关闭请求发送到驱动程序堆栈。 这三个请求的[请求类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_type)分别为**WdfRequestTypeCreate**、 **WdfRequestTypeCleanup**和**WdfRequestTypeClose**。

通常，除非你的驱动程序调用[**WdfDeviceInitSetExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive)，否则，驱动程序必须在收到文件创建、清除和关闭请求时执行特定于文件或其他特定于访问的操作，因为可以打开多个文件同时或多个应用程序可同时访问设备。 因此，该驱动程序必须跟踪与每个文件或应用程序相关联的 i/o 请求。

框架定义*框架文件对象*，这些对象表示用于访问设备的应用程序或驱动程序的方法，例如文件、目录、卷、邮件槽、命名管道或整个设备。 文件名可以与文件对象相关联，但文件名的含义是驱动程序特定的。 有关文件名的详细信息，请参阅[控制设备命名空间访问](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)。

如果你的驱动程序必须处理文件操作，则它必须从其[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数中调用[**WdfDeviceInitSetFileObjectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig) 。 **WdfDeviceInitSetFileObjectConfig**方法接收[**WDF\_FILEOBJECT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)结构作为输入。 驱动程序使用此结构来注册其[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)、 [*EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)和[*EvtFileClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)回调函数，并根据需要指示框架是否应在每次驱动程序接收文件创建请求。

处理文件操作的大多数驱动程序在框架文件对象的[上下文空间](framework-object-context-space.md)中存储特定于文件的信息。 如果驱动程序处理文件操作，但不需要将信息存储在文件对象的上下文空间中，则框架不必为驱动程序创建框架文件对象。

### <a name="creating-or-opening-a-file"></a>创建或打开文件

当框架收到针对函数驱动程序的文件创建请求时，它：

1.  创建一个表示该文件的框架文件对象，除非该驱动程序先前指出它不需要使用框架文件对象。

2.  如果驱动程序已注册回调函数，则调用驱动程序的[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调函数。

[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调函数通常获取有关文件的[信息](#obtaining-file-information)，如文件的名称和文件对象标志。 驱动程序通常将此信息存储在框架文件对象的上下文空间中。

驱动程序可以调用[**WdfDeviceConfigureRequestDispatching**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceconfigurerequestdispatching)来设置 i/o 队列来接收所有文件创建请求（**WdfRequestTypeCreate**请求类型），而不是提供[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调函数。 然后，该驱动程序将在队列的[*EvtIoDefault*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_default)请求处理程序中收到文件创建请求。 （如果队列的[**WDF\_IO\_queue\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)结构设置为**TRUE** **，则**i/o 队列无法接收文件创建请求。）

如果你的驱动程序未提供[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调函数，并且没有设置 i/o 队列来处理**WdfRequestTypeCreate**类型的 i/o 请求，框架：

-   如果驱动程序是函数驱动程序，则完成状态值为 "状态" 的所有文件创建请求\_"成功"。

-   如果驱动程序是筛选器驱动程序，则将所有文件创建请求转发到下一个较低的驱动程序。

（若要了解如何更改此行为，请参阅[**WDF\_FILEOBJECT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)结构中的**AutoForwardCleanupClose**成员。）

**请注意**   如果函数驱动程序未提供应用程序可用于访问驱动程序的设备的任何[设备接口](using-device-interfaces.md)，则驱动程序必须提供完成所有文件的[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调函数具有状态值的创建请求，其 NT\_成功（*状态*）等于**FALSE**。 否则，恶意应用程序可能会尝试使用设备的物理设备对象（PDO）的名称来访问设备。 （所有 PDOs 都有[名称](controlling-device-access-in-kmdf-drivers.md#naming-device-objects-only-when-necessary)。）

 

如果驱动程序将创建请求[转发](forwarding-i-o-requests.md)到 i/o 目标，则该驱动程序不能随后[完成](completing-i-o-requests.md)具有失败状态值的请求，除非该驱动程序从 i/o 目标接收到失败状态值。 否则，较低的驱动程序将不会收到创建请求失败的通知，并可能尝试操作，就像文件已打开一样。

如果驱动程序将创建请求转发到 i/o 目标，则驱动程序将无法设置[**WDF\_请求\_发送\_选项\_发送\_并\_忘记**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_send_options_flags)标志（如果框架已为创建请求。 因此，该驱动程序不能将 WDF\_请求\_发送\_选项\_发送\_和\_忘记标志，除非它还设置[**WdfFileObjectNotRequired**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_fileobject_class)标志。

请注意，如果驱动程序完成了一个具有错误状态的创建请求，则该框架将删除框架文件对象，但不会调用驱动程序的[*EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)或[*EvtFileClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)回调函数。 因此，如果驱动程序在文件对象的上下文空间之外分配额外的特定于对象的内存，则必须提供删除已分配内存的[*EvtCleanupCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)或[*EvtDestroyCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)回调函数。

对于 Windows Vista 和更高版本，可以[取消](canceling-i-o-requests.md)文件创建请求。 较早版本的 Windows 操作系统不支持取消文件创建请求。

对于来自用户应用程序的每个创建请求，系统始终会创建一个 Windows 驱动模型（WDM）文件对象。 如果驱动程序发送创建请求，则可能不会为该请求创建 WDM 文件对象。 通常，如果未提供 WDM 文件对象，则框架不创建框架文件对象。 但是，如果你的驱动程序调用了[**WdfDeviceInitSetExclusive**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetexclusive) ，并且如果驱动程序已在 WDF 的**FileObjectClass**成员中设置[**WdfFileObjectWdfCannotUseFsContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ne-wdfdevice-_wdf_fileobject_class) [ **\_FILEOBJECT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_fileobject_config)结构，即使某一 WDM 文件对象不存在，框架也将创建一个框架文件对象。

### <a href="" id="obtaining-file-information"></a>获取文件信息

驱动程序的[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)回调函数可调用以下一个或多个对象方法，以获取有关应用程序或驱动程序的设备访问权限的信息：

<a href="" id="---------wdffileobjectgetfilename--------"></a>[**WdfFileObjectGetFileName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetfilename)  
返回框架文件对象中包含的文件名。

<a href="" id="---------wdffileobjectgetflags--------"></a>[**WdfFileObjectGetFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetflags)  
返回框架文件对象中包含的标志。

<a href="" id="---------wdffileobjectwdmgetfileobject--------"></a>[**WdfFileObjectWdmGetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectwdmgetfileobject)  
返回与框架文件对象关联的 WDM 文件对象。

<a href="" id="---------wdfrequestgetparameters--------"></a>[**WdfRequestGetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetparameters)  
检索与框架请求对象关联的参数。 如果[请求类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ne-wdfrequest-_wdf_request_type)为**WdfRequestTypeCreate**，则[**请求\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_parameters)结构中包含有关文件创建请求的信息\_ **。**

通常，驱动程序在框架文件对象的上下文空间中存储文件信息。 当驱动程序从一个 i/o 队列获取 i/o 请求时，驱动程序可以调用[**WdfRequestGetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetfileobject)来获取与该请求关联的框架文件对象的句柄。 然后，该驱动程序可以检索存储在框架文件对象上下文空间中的文件信息。

你的驱动程序可以通过调用[**WdfIoQueueRetrieveRequestByFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueueretrieverequestbyfileobject)在 i/o 队列中搜索与特定文件关联的请求。

如果你的驱动程序具有指向 WDM[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构的指针，则驱动程序可以调用[**WdfDeviceGetFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetfileobject)来获取与 wdm 设备对象相关联的框架文件对象的句柄。

### <a name="closing-a-file"></a>关闭文件

当某个应用程序或另一个驱动程序关闭某个文件时，框架会接收清理请求和驱动程序的关闭请求。 框架：

1.  如果驱动程序已注册了这些回调函数，则调用驱动程序的[*EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)和[*EvtFileClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)回调函数。

2.  删除表示文件的框架文件对象。

驱动程序的[*EvtFileCleanup*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_cleanup)和[*EvtFileClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_file_close)回调函数接收框架文件对象的句柄。 驱动程序可以调用[**WdfFileObjectGetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetdevice)来确定哪个框架设备对象与框架文件对象相关联。

 

 





