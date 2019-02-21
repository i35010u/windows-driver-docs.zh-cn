---
Description: Supporting Client Contexts
title: 支持客户端上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b227917f936a9f0a0136e786b06b4bd91ea39c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545779"
---
# <a name="supporting-client-contexts"></a>支持客户端上下文


Windows 便携式设备 (WPD) 驱动程序提供了应用程序和物理设备之间的通信通道。 可以在任何时间运行的多个 WPD 应用程序。 该驱动程序必须处理来自不同的计算机上的客户端的请求，并确定基于排队的请求的客户端。 换而言之，驱动程序需要一种高效、 更轻松的方法，按每个连接来存储客户端数据和检索请求数据。

用户模式驱动程序 Frameork (UMDF) 支持此功能使用的上下文区域： 驱动程序将在其中保存客户端数据的通用机制。 WPD 驱动程序应分配的数据结构或对象以保存客户端数据，为 framework 对象的上下文区域分配数据结构并在更高版本时检索的上下文。

每个连接 WDF framework 对象使用相应是 WDF 文件对象。

## <a name="span-idassigningthecontextspanspan-idassigningthecontextspanspan-idassigningthecontextspanassigning-the-context"></a><span id="Assigning_the_Context"></span><span id="assigning_the_context"></span><span id="ASSIGNING_THE_CONTEXT"></span>分配上下文


当客户端计算机打开与它的连接时，驱动程序将分配上下文。

当 WPD 程序调用**IPortableDevice::Open**或**IPortableDeviceService::Open**方法时，WPD API 创建的句柄驱动程序通过使用 Win32 **CreateFile**方法。 在驱动程序方面，用户模式驱动程序 Frameork (UMDF) 初始化**IWDFFile**对象，并将其，以及对驱动程序的创建请求转发**IQueueCallbackCreate::OnCreateFile**方法。 **IWDFFile**对象在这种情况下表示 Win32**处理**用于此客户端驱动程序的后续通信。

您可以找到的一个示例**CreateFile**回调实现中 WpdWudfSampleDriver **CQueue::OnCreateFile**方法。 特定于驱动程序 ContextMap COM 对象用于存储客户端数据 （应用程序名称、 版本、 正在进行枚举和资源上下文等）。 请注意，使用了 COM 对象，如 UMDF; 不需要的上下文数据UMDF 看到上下文数据作为**PVOID**。 如果使用的 COM 对象来存储上下文数据，您的驱动程序必须维护的 COM 对象的引用计数，并确保在适当的清除方法中释放其资源。

若要保存的上下文数据，该驱动程序初始化新的 ContextMap 对象，并调用**IWDFObject::AssignContext**方法**IWDFFile** UMDF 传递的对象。 此方法的参数是指向**IObjectCleanup**对象和新创建的 ContextMap。 **IObjectCleanup**对象包含上下文清理代码; 新创建的映射包含存储的数据。 驱动程序调用**IObjectCleanup::OnCleanup**期间 CloseHandle 破坏文件对象的方法。

此外，只有一个上下文可以分配给文件对象 （或任何 UMDF framework 对象）。 对后续调用**AssignContext**方法失败，如果已经分配了上下文。 若要添加或删除特定于客户端的数据动态，驱动程序可以实现的映射对象来管理数据以及为文件对象的上下文指针分配给该对象。 有关示例，请参阅 WpdWudfSampleDriver ContextMap 对象。

## <a name="span-idretrievingandsavingcontextdataspanspan-idretrievingandsavingcontextdataspanspan-idretrievingandsavingcontextdataspanretrieving-and-saving-context-data"></a><span id="Retrieving_and_Saving_Context_Data"></span><span id="retrieving_and_saving_context_data"></span><span id="RETRIEVING_AND_SAVING_CONTEXT_DATA"></span>检索和保存的上下文数据


若要在请求期间访问客户端数据，WPD 驱动程序检索上下文从给定**IWDFFile**对象。

检索序列是通过完成以下步骤来实现的：

1.  驱动程序调用**IWDFIoRequest::GetFileObject**方法来获取**IWDFFile**对象。
2.  驱动程序调用**IWDFObject::RetrieveContext**方法**IWDFFile**若要访问上下文区域的对象。 在示例驱动程序的上下文区域是 ContextMap 对象中创建指向**CQueue::OnCreateFile**应用程序的调用时**IPortableDevice::Open**。
3.  该驱动程序添加数据，或删除数据从 ContextMap 对象直接处理 WPD 命令时。 每次应用程序连接通过调用**IPortableDevice::Open**，它将具有其自己**IWDFFile**和 ContextMap 对象。

请参阅代码从 WpdWudfSampleDriver 有关如何检索上下文映射并添加客户端信息的示例。 下表描述了在哪里可以找到代码中 WpdWudfSampleDriver。

| 示例                                                                                                                  | 示例驱动程序中的位置           |
|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| 从 WDF 请求的文件对象中检索上下文映射。                                                     | **CQueue::OnDeviceIoControl**       |
| 将客户端信息添加到上下文映射，当处理 WPD\_命令\_常见\_保存\_客户端\_信息命令 | **WpdBaseDriver::OnSaveClientInfo** |

 

## <a name="span-idreleasingthecontextspanspan-idreleasingthecontextspanspan-idreleasingthecontextspanreleasing-the-context"></a><span id="Releasing_the_Context"></span><span id="releasing_the_context"></span><span id="RELEASING_THE_CONTEXT"></span>释放上下文


当客户端应用程序调用**IPortableDevice::Close**方法，WPD API 又调用**CloseHandle**上与打开的连接关联的 Win32 句柄。 UMDF 销毁之前**IWDFFile**对象以响应**CloseHandle**，它调用该文件对象的**IObjectCleanup::OnCleanup**方法，该驱动程序传递到方法**AssignContext**期间**OnCreateFile**。

实现示例**IQueueCleanup**回调是 WpdWudfSampleDriver 驱动程序**CQueue::OnCleanup**方法。 此方法检索存储在 IWDFObject 对象 ContextMap (在此情况下，实例从 IWDFFile **OnCreateFile**) 并释放已分配的内存，包括 ContextMap 保存的对象。 若要避免内存泄漏，请确保正确清理，和 （如果适用） 递减引用计数对象。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





