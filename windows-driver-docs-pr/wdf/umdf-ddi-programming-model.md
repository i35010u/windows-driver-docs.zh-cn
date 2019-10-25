---
title: UMDF DDI 编程模型
description: UMDF DDI 编程模型
ms.assetid: d4bf0791-d2c4-4504-84ad-020880124363
keywords:
- UMDF 对象 WDK，DDI
- framework 对象 WDK UMDF，DDI
- UMDF DDI WDK
- DDI WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c4c8981385b75875ab44db2715834d03e2c7c6d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831602"
---
# <a name="umdf-ddi-programming-model"></a>UMDF DDI 编程模型


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架和 UMDF 驱动程序通过 UMDF DDI 进行通信。 UMDF DDI 类似于 KMDF DDI，只不过 UMDF DDI 基于 COM。 因此，熟悉 KMDF 的驱动程序编写器将了解 UMDF。

对于每种类型的框架对象，UMDF 都定义了一个接口，通过该接口操作对象的实例。 每个接口都支持方法和属性。 方法定义可代表对象和属性来执行的操作，并检索对象的特征。 某些接口由框架实现，其他接口由驱动程序实现。 框架对象公开的接口的形式为 IWDF&lt;object&gt;，而驱动程序公开的事件回调接口的格式为 I&lt;object&gt;&lt;操作&gt;，其中 &lt;对象&gt; 表示队列、请求等，&lt;操作&gt; 指示接口的作用。 回调接口的方法以 "On" 开头。

UMDF 驱动程序通过其方法和属性与框架的对象通信。 框架通过事件通知与驱动程序通信，事件通知是框架可调用以通知驱动程序特定事件的回调函数。 若要注册回调函数，驱动程序可以调用以下框架对象方法，并可以将指针传递给与驱动程序所支持的回调函数的所有接口相关联的**IUnknown**接口。

-   [**IWDFDevice::CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)

-   [**IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)

-   [**IWDFDriver::CreateWdfObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createwdfobject)

作为框架通信驱动程序的示例，请考虑设备的默认 i/o 队列对象。 驱动程序可以调用方法（如[**IWDFIoQueue：： GetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-getstate)）来检索有关 i/o 队列的状态信息，或使用[**IWDFIoQueue：： RetrieveNextRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfioqueue-retrievenextrequest)来检索 i/o 队列的请求。 驱动程序还可以通过调用[**IWDFDevice：： CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)方法来注册回调接口（如[IQueueCallbackRead](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackread)和[IQueueCallbackWrite](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackwrite)），请求 i/o 队列上的通知。 当应用程序发送读取和写入请求时，框架随后会调用这些接口的方法。

该框架提供了跨驱动程序回调方法所需的任何同步。 默认情况下，框架在设备对象级别进行同步;也就是说，框架不会同时调用设备对象级别或其下的事件回调方法。 驱动程序可以通过请求不同步来覆盖此默认值。 有关详细信息，请参阅[指定回调同步模式](specifying-a-callback-synchronization-mode.md)。

 

 





