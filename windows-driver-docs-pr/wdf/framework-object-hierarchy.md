---
title: 框架对象层次结构
description: 框架对象层次结构
ms.assetid: ffacca8f-4083-4998-83d2-7c31544eb497
keywords:
- UMDF 对象 WDK，层次结构
- 框架对象 WDK UMDF、层次结构
- 层次结构 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 216574d417b252560588f8e414be9d93c3032226
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843120"
---
# <a name="framework-object-hierarchy"></a>框架对象层次结构


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

下图显示了父子框架对象层次结构。

![umdf 父子对象层次结构](images/umdfhierarchy.gif)

框架对象的生存期范围由它们在层次结构中的位置确定，以及如何创建这些对象。 框架对象的生存期范围属于以下类别之一：

-   框架控制对象的创建和析构。

    框架创建并销毁对象，如[驱动程序对象](framework-driver-object.md)和[设备对象](framework-device-object.md)，以响应系统事件。 当用户模式驱动程序调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法来创建设备对象时，驱动程序可以选择注册以便在销毁设备对象之前由框架接收通知。

-   框架创建对象;但是，驱动程序会控制释放对象的时间。

    当向驱动程序提供 i/o 时， [i/o 请求对象](framework-i-o-request-object.md)遵循此模式。 框架创建 request 对象，请求对象的生存期有效，直到驱动程序调用[**IWDFIoRequest：： Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)方法。

-   驱动程序创建对象并将对象与另一个框架对象相关联。

    某些框架对象是通过父框架对象实例公开的，此方法由要与生存期管理的对象关联的父框架对象实例公开。 [**IWDFDevice：： CreateIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)方法是此模式的一个示例。 如果对**IWDFDevice：： CreateIoQueue**的调用成功，则新创建的 i/o 队列将与[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)接口表示的设备实例相关联。 当父对象被销毁时，框架会自动清除子实例。 如果驱动程序向框架注册适当的回调函数，则会向驱动程序通知这些事件。

 

 





