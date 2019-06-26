---
title: UMDF DDI 编程模型
description: UMDF DDI 编程模型
ms.assetid: d4bf0791-d2c4-4504-84ad-020880124363
keywords:
- UMDF 对象 WDK DDI
- framework 对象 WDK UMDF DDI
- UMDF DDI WDK
- DDI WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2085af1a240daa48edc265cd4a40d2ddf3d4cd99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372301"
---
# <a name="umdf-ddi-programming-model"></a>UMDF DDI 编程模型


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架和 UMDF 驱动程序通过 UMDF DDI 进行通信。 UMDF DDI 是类似于 KMDF DDI 只不过 UMDF DDI 基于 com。 因此，熟悉 KMDF 驱动程序编写人员将了解 UMDF。

对于每种类型的 framework 对象，UMDF 定义一个用来操作对象的实例接口。 每个接口支持的方法和属性。 方法定义可以代表对象执行的操作和属性将设置和检索对象的特征。 由框架实现某些接口以及其他驱动程序实现。 由框架对象公开的接口是窗体 IWDF&lt;对象&gt;，而窗体的驱动程序公开的事件回调接口是我&lt;对象&gt;&lt;操作&gt;，其中&lt;对象&gt;表示队列、 请求和等等，以及&lt;操作&gt;指示该接口的用途。 回调接口的方法都以"On"开头。

与框架的对象进行通信 UMDF 驱动程序通过其方法和属性。 该框架与通过事件通知，都是框架就可以调用以通知有关特定事件驱动程序的回调函数的驱动程序进行通信。 若要注册回调函数，该驱动程序可以调用，例如，以下 framework 对象的方法和可以传递一个指向**IUnknown**接口关联的所有接口的回调函数的驱动程序支持。

-   [**IWDFDevice::CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)

-   [**IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)

-   [**IWDFDriver::CreateWdfObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject)

作为到框架的通信的驱动程序示例，请考虑设备的默认 I/O 队列对象。 驱动程序可以调用方法，如[ **IWDFIoQueue::GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfioqueue-getstate)来检索有关 I/O 队列的状态信息或[ **IWDFIoQueue::RetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfioqueue-retrievenextrequest)从 I/O 队列中检索请求。 驱动程序还可以通过调用请求有关的 I/O 队列通知[ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)方法来注册回调接口，如[IQueueCallbackRead](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackread)并[IQueueCallbackWrite](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackwrite)。 这些接口方法随后由框架时调用应用程序发送读取和写入请求。

该框架提供任何需要的驱动程序的回调方法的同步。 默认情况下，框架将同步设备对象级别;也就是说，框架不同时调用事件回叫方法或设备对象级别以下。 驱动程序可以通过请求没有进行的同步来覆盖此默认值。 有关详细信息，请参阅[指定回调同步模式](specifying-a-callback-synchronization-mode.md)。

 

 





