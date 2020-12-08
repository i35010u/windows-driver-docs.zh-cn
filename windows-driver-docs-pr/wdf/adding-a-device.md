---
title: 添加设备
description: 添加设备
keywords:
- User-Mode Driver Framework WDK，添加设备
- UMDF WDK，添加设备
- 用户模式驱动程序 WDK UMDF，添加设备
- 安装设备 WDK、UMDF
- 添加设备 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: feafb8c4e770ac82000bc389701f467723049f36
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815797"
---
# <a name="adding-a-device"></a>添加设备


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架为驱动程序主机进程中加载的每个设备添加一个设备对象。 为了添加设备，框架将调用驱动程序的 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 方法，并在调用中传递 [IWDFDriver](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver) 和 [IWDFDeviceInitialize](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize) 接口。 仅当驱动程序调用 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)后，提供的 **IWDFDeviceInitialize** 接口才有效。 驱动程序可以调用 **IWDFDeviceInitialize** 的以下方法来执行以下操作：

-   驱动程序调用 [**IWDFDeviceInitialize：： RetrieveDevicePropertyStore**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore) 方法来检索设备属性存储的 [IWDFNamedPropertyStore](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfnamedpropertystore) 接口。 驱动程序可以使用 **IWDFNamedPropertyStore** 来检索和设置设备的属性。

-   驱动程序调用 [**IWDFDeviceInitialize：： SetLockingConstraint**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint) 方法，以指定框架如何调用回调函数。

-   驱动程序调用 [**IWDFDeviceInitialize：： SetFilter**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter) 方法将设备作为筛选器设备启用。

驱动程序使用 [IWDFDeviceInitialize](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdeviceinitialize)初始化设备后，驱动程序会在对 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法的调用中传递一个指向 **IWDFDeviceInitialize** 的指针，以便为设备创建一个 [UMDF 设备对象](framework-device-object.md)。 创建框架设备对象之后，驱动程序将调用 [**IWDFDevice：： CreateIoQueue**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createioqueue) 方法来创建读写 i/o 队列。 在这些 **IWDFDevice：： CreateIoQueue** 调用中，驱动程序必须确定它如何从 i/o 队列接收请求。 有关详细信息，请参阅为 [I/o 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md)。

 

