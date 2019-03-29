---
title: 框架对象层次结构
description: 框架对象层次结构
ms.assetid: ffacca8f-4083-4998-83d2-7c31544eb497
keywords:
- UMDF 对象 WDK，层次结构
- framework 对象 WDK UMDF，层次结构
- 层次结构 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cb32efe1088b3a9deafe26087751f56120f9a49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576674"
---
# <a name="framework-object-hierarchy"></a>框架对象层次结构


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下图显示了父-子 framework 对象层次结构。

![umdf 父-子对象层次结构](images/umdfhierarchy.gif)

Framework 对象的生存期范围取决于它们中的层次结构和创建对象的方式的位置。 Framework 对象的生存期范围划分为以下类别之一：

-   框架控制创建和销毁的对象。

    框架将创建和销毁对象，如[驱动程序对象](framework-driver-object.md)并[设备对象](framework-device-object.md)，以响应系统事件。 当用户模式驱动程序调用[ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)方法来创建设备对象，该驱动程序可以选择注册的设备对象之前由框架通知销毁。

-   框架将创建的对象;但是，该驱动程序控制时释放的对象。

    [I/O 请求对象](framework-i-o-request-object.md)I/O 提供给该驱动程序时应遵循此模式。 框架将创建的请求对象，和之前的驱动程序调用 request 对象的生存期都有效[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)方法。

-   该驱动程序创建对象，并将该对象与另一个框架对象相关联。

    某些 framework 对象创建对象的生存期管理用于关联到一个父框架对象实例公开的方法。 [ **IWDFDevice::CreateIoQueue** ](https://msdn.microsoft.com/library/windows/hardware/ff557020)方法是此模式的一个示例。 如果调用**IWDFDevice::CreateIoQueue**成功，新创建 I/O 队列是关联与设备实例[IWDFDevice](https://msdn.microsoft.com/library/windows/hardware/ff556917)接口表示。 当父对象被销毁后时，框架将自动清理子实例。 这些事件的情况下，如果驱动程序向框架注册相应的回调函数，驱动程序会收到通知。

 

 





