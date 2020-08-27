---
description: 支持客户端上下文
title: 支持客户端上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4612d46e8f3bbacb857cc762b03796f1905aaf06
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968506"
---
# <a name="supporting-client-contexts"></a>支持客户端上下文


 (WPD) 驱动程序的 Windows 便携式设备在应用程序和物理设备之间提供通信通道。 随时可以运行多个 WPD 应用程序。 驱动程序需要处理来自计算机上不同客户端的请求，并根据排队的请求来识别客户端。 换句话说，驱动程序需要一种基于连接按连接来存储客户端数据的简单简单的方法，并在请求时检索数据。

用户模式驱动程序 Frameork (UMDF) 通过使用上下文区域支持此功能：驱动程序保存客户端数据的通用机制。 WPD 驱动程序应分配一个数据结构或对象用于保存客户端数据，将数据结构分配给框架对象的上下文区域，以后再检索上下文。

要使用的每个连接的 WDF 框架对象均为 WDF 文件对象。

## <a name="span-idassigning_the_contextspanspan-idassigning_the_contextspanspan-idassigning_the_contextspanassigning-the-context"></a><span id="Assigning_the_Context"></span><span id="assigning_the_context"></span><span id="ASSIGNING_THE_CONTEXT"></span>分配上下文


驱动程序在客户端计算机打开与之的连接时分配上下文。

当 WPD 应用程序调用 **IPortableDevice：： open** 或 **IPortableDeviceService：： open** 方法时，WPD API 使用 Win32 **CreateFile** 方法创建驱动程序的句柄。 在驱动程序端，用户模式驱动程序 Frameork (UMDF) 初始化一个 **IWDFFile** 对象，并将该对象连同创建请求一起转发给驱动程序的 **IQueueCallbackCreate：： OnCreateFile** 方法。 在此示例中， **IWDFFile** 对象表示用于从此客户端到驱动程序的后续通信的 Win32 **句柄** 。

可在 WpdWudfSampleDriver 的**CQueue：： OnCreateFile**方法中找到**CreateFile**回调实现的示例。 驱动程序特定的 ContextMap COM 对象用于存储客户端数据 (应用程序名称、版本、正在进行枚举和资源上下文等) 。 请注意，UMDF 不需要使用 COM 对象作为上下文数据;UMDF 将上下文数据视为 **PVOID**。 如果使用 COM 对象来存储上下文数据，则驱动程序必须维护该 COM 对象的引用计数，并确保在适当的清理方法中释放其资源。

为了保存上下文数据，驱动程序将初始化一个新的 ContextMap 对象，并为 UMDF 传入的**IWDFFile**对象调用**IWDFObject：： AssignContext**方法。 此方法的参数是指向 **IObjectCleanup** 对象的指针和新创建的 ContextMap。 **IObjectCleanup**对象包含上下文清理代码;新创建的映射包含要存储的数据。 如果文件对象在 CloseHandle 期间销毁，驱动程序将调用 **IObjectCleanup：： OnCleanup** 方法。

此外，只能将一个上下文分配给 file 对象 (或) 任何 UMDF framework 对象。 如果已分配上下文，则对 **AssignContext** 方法的后续调用会失败。 若要动态添加或删除客户端特定的数据，驱动程序可以实现一个映射对象来管理数据并将指向该对象的指针分配为文件对象的上下文。 有关示例，请参阅 WpdWudfSampleDriver 的 ContextMap 对象。

## <a name="span-idretrieving_and_saving_context_dataspanspan-idretrieving_and_saving_context_dataspanspan-idretrieving_and_saving_context_dataspanretrieving-and-saving-context-data"></a><span id="Retrieving_and_Saving_Context_Data"></span><span id="retrieving_and_saving_context_data"></span><span id="RETRIEVING_AND_SAVING_CONTEXT_DATA"></span>检索和保存上下文数据


若要在请求期间访问客户端数据，WPD 驱动程序将从给定的 **IWDFFile** 对象检索上下文。

检索序列是通过完成以下步骤来完成的：

1.  驱动程序调用 **IWDFIoRequest：： GetFileObject** 方法来获取 **IWDFFile** 对象。
2.  驱动程序调用**IWDFFile**对象上的**IWDFObject：： RetrieveContext**方法来访问上下文区域。 在示例驱动程序中，上下文区域是指向 ContextMap 对象的指针，该对象是在应用程序调用**IPortableDevice：： Open**时在**CQueue：： OnCreateFile**中创建的。
3.  驱动程序在处理 WPD 命令时直接在 ContextMap 对象中添加或删除数据。 每次应用程序通过调用 **IPortableDevice：： Open**进行连接时，它都具有自己的 **IWDFFile** 和 ContextMap 对象。

有关如何检索上下文映射和添加客户端信息的示例，请参阅 WpdWudfSampleDriver 中的代码。 下表描述了可在 WpdWudfSampleDriver 中查找代码的位置。

| 示例                                                                                                                  | 示例驱动程序中的位置           |
|--------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| 正在从 WDF 请求的文件对象检索上下文映射。                                                     | **CQueue::OnDeviceIoControl**       |
| 处理 WPD 命令时将客户端信息添加到上下文 \_ 映射 \_ 公共 \_ 保存 \_ 客户端 \_ 信息命令 | **WpdBaseDriver::OnSaveClientInfo** |

 

## <a name="span-idreleasing_the_contextspanspan-idreleasing_the_contextspanspan-idreleasing_the_contextspanreleasing-the-context"></a><span id="Releasing_the_Context"></span><span id="releasing_the_context"></span><span id="RELEASING_THE_CONTEXT"></span>正在释放上下文


当客户端应用程序调用 **IPortableDevice：： Close** 方法时，WPD API 将在与打开的连接关联的 Win32 句柄上调用 **CloseHandle** 。 在 UMDF 销毁**IWDFFile**对象以响应**CloseHandle**之前，它将调用文件对象的**IObjectCleanup：： OnCleanup**方法，驱动程序会在**AssignContext**过程中将该方法传递到**OnCreateFile** 。

**IQueueCleanup**回调的示例实现是 WpdWudfSampleDriver 驱动程序的**CQueue：： OnCleanup**方法。 此方法检索 IWDFObject 对象中存储的 ContextMap， (在本例中，IWDFFile **OnCreateFile**) 的实例，并释放分配的内存，包括 ContextMap 包含的对象。 若要避免内存泄漏，请确保已正确清除对象，如果适用) 减少引用计数，则 (。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





