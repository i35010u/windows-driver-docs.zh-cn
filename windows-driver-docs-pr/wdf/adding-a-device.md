---
title: 添加设备
description: 添加设备
ms.assetid: 233e3315-3044-42d7-867c-0a9e153eb53b
keywords:
- 用户模式驱动程序框架 WDK，添加设备
- UMDF WDK，添加设备
- 用户模式驱动程序 WDK UMDF，添加设备
- 安装设备 WDK、UMDF
- 添加设备 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a79b5ada631f1e91d70260d406a07f168928e5d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191249"
---
# <a name="adding-a-device"></a>添加设备


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架为驱动程序主机进程中加载的每个设备添加一个设备对象。 为了添加设备，框架将调用驱动程序的 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 方法，并在调用中传递 [IWDFDriver](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver) 和 [IWDFDeviceInitialize](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize) 接口。 仅当驱动程序调用[**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)后，提供的**IWDFDeviceInitialize**接口才有效。 驱动程序可以调用 **IWDFDeviceInitialize** 的以下方法来执行以下操作：

-   驱动程序调用 [**IWDFDeviceInitialize：： RetrieveDevicePropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore) 方法来检索设备属性存储的 [IWDFNamedPropertyStore](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore) 接口。 驱动程序可以使用 **IWDFNamedPropertyStore** 来检索和设置设备的属性。

-   驱动程序调用 [**IWDFDeviceInitialize：： SetLockingConstraint**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint) 方法，以指定框架如何调用回调函数。

-   驱动程序调用 [**IWDFDeviceInitialize：： SetFilter**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter) 方法将设备作为筛选器设备启用。

驱动程序使用[IWDFDeviceInitialize](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)初始化设备后，驱动程序会在对[**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法的调用中传递一个指向**IWDFDeviceInitialize**的指针，以便为设备创建一个[UMDF 设备对象](framework-device-object.md)。 创建框架设备对象之后，驱动程序将调用 [**IWDFDevice：： CreateIoQueue**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue) 方法来创建读写 i/o 队列。 在这些 **IWDFDevice：： CreateIoQueue** 调用中，驱动程序必须确定它如何从 i/o 队列接收请求。 有关详细信息，请参阅为 [I/o 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md)。

 

