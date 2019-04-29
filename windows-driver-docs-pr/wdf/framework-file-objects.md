---
title: 框架文件对象
description: 框架文件对象
ms.assetid: 93ec5dd7-8ef0-4cea-9253-ea5d7869d4b8
keywords:
- I/O 请求 WDK KMDF，文件对象
- 文件对象 WDK KMDF
- 请求处理 WDK KMDF，文件对象
- framework 对象 WDK KMDF，文件对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2b08ac687648f3747082f6f6d47a89ab26f3637
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391348"
---
# <a name="framework-file-objects"></a>框架文件对象





当应用程序或驱动程序尝试访问设备时，通常通过创建或打开一个文件，操作系统将发送的文件创建请求到驱动程序堆栈。 应用程序或驱动程序完成后使用该设备，系统将发送文件清理并关闭驱动程序堆栈的请求。 [请求类型](https://msdn.microsoft.com/library/windows/hardware/ff552503)的以下三个请求都**WdfRequestTypeCreate**， **WdfRequestTypeCleanup**，以及**WdfRequestTypeClose**，分别。

通常情况下，除非您的驱动程序已调用[ **WdfDeviceInitSetExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff546097)、 驱动程序必须执行特定于文件或其他特定于访问的操作时接收文件创建、 清理和关闭请求，因为多个文件可以同时打开或多个应用程序可以同时访问设备。 该驱动程序必须因此跟踪的每个文件或应用程序与关联的 I/O 请求。

该框架定义*framework 文件对象*，表示应用程序或驱动程序的方式访问的设备，如文件、 目录、 卷、 邮件槽、 命名管道或整个设备。 文件名称可以是与文件对象，但文件名称的含义是特定于驱动程序。 有关文件的名称的详细信息，请参阅[控制设备 Namespace 访问](https://msdn.microsoft.com/library/windows/hardware/ff542068)。

如果您的驱动程序必须处理文件操作，它必须调用[ **WdfDeviceInitSetFileObjectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff546107)中其[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调函数。 **WdfDeviceInitSetFileObjectConfig**方法接收[ **WDF\_的文件对象\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551319)结构作为输入。 该驱动程序使用此结构来注册其[ *EvtDeviceFileCreate*](https://msdn.microsoft.com/library/windows/hardware/ff540868)， [ *EvtFileCleanup*](https://msdn.microsoft.com/library/windows/hardware/ff541700)，和[ *EvtFileClose* ](https://msdn.microsoft.com/library/windows/hardware/ff541702)回调函数和 （可选） 若要指示框架是否应创建框架文件对象每次驱动程序收到的文件创建请求。

处理文件操作的大多数驱动程序存储特定于文件的信息的框架文件对象中[上下文空间](framework-object-context-space.md)。 如果您的驱动程序处理文件操作，但不需要将信息存储在文件对象的上下文空间，则不需要创建框架文件对象的驱动程序框架。

### <a name="creating-or-opening-a-file"></a>创建或打开文件

当框架接收函数驱动程序、 文件创建请求时它：

1.  创建的框架文件对象来表示该文件，除非该驱动程序以前指示，它不需要使用框架文件对象。

2.  调用您的驱动程序[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)回调函数，如果该驱动程序已注册的回调函数。

[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)回调函数通常[获取信息](#obtaining-file-information)有关该文件，如其名称和文件对象标志。 驱动程序通常将此信息存储在框架文件对象的上下文空间中。

而不是提供[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)驱动程序可以调用回调函数[ **WdfDeviceConfigureRequestDispatching** ](https://msdn.microsoft.com/library/windows/hardware/ff545920)用于设置 I/O 队列来接收所有文件创建请求 (**WdfRequestTypeCreate**请求类型)。 该驱动程序随后将在队列中接收文件创建请求[ *EvtIoDefault* ](https://msdn.microsoft.com/library/windows/hardware/ff541757)请求处理程序。 (如果 I/O 队列不能接收文件创建请求**DefaultQueue**的队列的成员[ **WDF\_IO\_队列\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff552359)结构设置为**TRUE**。)

如果您的驱动程序未提供[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)回调函数而不会不设置 I/O 队列以处理**WdfRequestTypeCreate**-键入 I/O 请求framework:

-   完成的状态将 status 值驱动程序的所有文件创建请求\_成功后，如果您的驱动程序函数的驱动程序。

-   所有文件创建将请求都转发到下一个较低的驱动程序，如果您的驱动程序是一个筛选器驱动程序。

(若要查看如何可以更改此行为，请参阅**AutoForwardCleanupClose**的成员[ **WDF\_的文件对象\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551319)结构。)

**请注意**  如果您函数的驱动程序不提供任何[设备接口](using-device-interfaces.md)，应用程序可以使用访问驱动程序的设备，该驱动程序必须提供[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)完成所有的回调函数的文件将 status 值创建请求的 NT\_成功 (*状态*) 等于**FALSE**. 否则，恶意应用程序可能尝试访问的设备使用设备的物理设备对象 (PDO) 的名称。 (具有所有 PDOs[名称](controlling-device-access-in-kmdf-drivers.md#naming-device-objects-only-when-necessary)。)

 

如果驱动程序[转发](forwarding-i-o-requests.md)到 I/O 的目标的创建请求，该驱动程序必须随后不[完整](completing-i-o-requests.md)具有失败状态的请求值，除非该驱动程序从 I/O 接收失败状态值目标。 否则，较低的驱动程序将不会通知创建请求失败，可能会尝试运行时文件处于打开状态。

如果驱动程序将转发到 I/O 的目标的创建请求时，不能设置驱动程序[ **WDF\_请求\_发送\_选项\_发送\_AND\_忘记** ](https://msdn.microsoft.com/library/windows/hardware/ff552493)标志，如果该框架已创建用于创建请求的框架文件对象。 因此，该驱动程序不能设置 WDF\_请求\_发送\_选项\_发送\_AND\_忘记标志，用于创建请求，除非还设置[ **WdfFileObjectNotRequired** ](https://msdn.microsoft.com/library/windows/hardware/ff551315)标志。

请注意，如果驱动程序完成后使用的错误状态的创建请求，该框架框架文件对象中删除但不会调用驱动程序的[ *EvtFileCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff541700)或[ *EvtFileClose* ](https://msdn.microsoft.com/library/windows/hardware/ff541702)回调函数。 因此，如果驱动程序分配了额外特定于对象的内存以外的文件对象的上下文空间它必须提供[ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)或[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)删除已分配的内存的回调函数。

适用于 Windows Vista 及更高版本，可以是文件创建请求[取消](canceling-i-o-requests.md)。 早期版本的 Windows 操作系统不支持取消文件创建请求。

系统始终会创建每个创建请求的来自用户应用程序的 Windows 驱动程序模型 (WDM) 文件对象。 如果驱动程序发送创建请求，可能会创建请求的 WDM 文件对象。 通常情况下，该框架不会创建框架文件对象不存在 WDM 文件对象。 但是，如果您的驱动程序已调用[ **WdfDeviceInitSetExclusive** ](https://msdn.microsoft.com/library/windows/hardware/ff546097)如果驱动程序已设置[ **WdfFileObjectWdfCannotUseFsContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff551315)中**FileObjectClass**的成员[ **WDF\_文件对象\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff551319)结构，该框架将创建框架文件对象即使 WDM 文件对象不存在。

### <a href="" id="obtaining-file-information"></a> 获取文件信息

在驱动程序[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)回调函数可以调用一个或多个以下的对象方法，以获取有关应用程序或驱动程序的访问的设备信息：

<a href="" id="---------wdffileobjectgetfilename--------"></a>[**WdfFileObjectGetFileName**](https://msdn.microsoft.com/library/windows/hardware/ff547310)  
返回框架文件对象中包含的文件名称。

<a href="" id="---------wdffileobjectgetflags--------"></a>[**WdfFileObjectGetFlags**](https://msdn.microsoft.com/library/windows/hardware/ff547316)  
返回框架文件对象中包含的标志。

<a href="" id="---------wdffileobjectwdmgetfileobject--------"></a>[**WdfFileObjectWdmGetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff547324)  
返回与框架文件对象相关联的 WDM 文件对象。

<a href="" id="---------wdfrequestgetparameters--------"></a>[**WdfRequestGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549969)  
检索与框架请求对象相关联的参数。 如果[请求类型](https://msdn.microsoft.com/library/windows/hardware/ff552503)是**WdfRequestTypeCreate**，则**Parameters.Create**隶属[ **WDF\_请求\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff552472)结构包含有关文件创建请求的信息。

通常情况下，该驱动程序框架文件对象的上下文空间中存储文件的信息。 在您的驱动程序从一个 if 其 I/O 队列中获取的 I/O 请求，该驱动程序可以调用[ **WdfRequestGetFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff549963)若要获取的句柄与请求关联的框架文件对象。 然后，驱动程序可以检索存储在框架文件对象的上下文空间中的文件信息。

您的驱动程序可以搜索通过调用特定的文件与相关联的请求的 I/O 队列[ **WdfIoQueueRetrieveRequestByFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff548470)。

如果您的驱动程序都有指向 WDM [**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构，该驱动程序可以调用[ **WdfDeviceGetFileObject** ](https://msdn.microsoft.com/library/windows/hardware/ff546007)若要获取的句柄与 WDM 设备对象相关联的框架文件对象。

### <a name="closing-a-file"></a>关闭文件

当应用程序或另一个驱动程序关闭文件时，框架将接收清理请求和您的驱动程序的关闭请求。 Framework:

1.  调用您的驱动程序[ *EvtFileCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff541700)并[ *EvtFileClose* ](https://msdn.microsoft.com/library/windows/hardware/ff541702)回调函数，如果该驱动程序已注册这些回调函数。

2.  删除表示的文件的框架文件对象。

在驱动程序[ *EvtFileCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff541700)并[ *EvtFileClose* ](https://msdn.microsoft.com/library/windows/hardware/ff541702)回调函数接收框架文件对象的句柄。 该驱动程序可以调用[ **WdfFileObjectGetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff547302)若要确定哪个 framework 设备对象与框架文件对象相关联。

 

 





