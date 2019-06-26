---
title: 添加设备
description: 添加设备
ms.assetid: 233e3315-3044-42d7-867c-0a9e153eb53b
keywords:
- 添加设备的用户模式驱动程序框架 WDK
- UMDF WDK、 添加设备
- 用户模式驱动程序 WDK UMDF，添加设备
- 安装设备 WDK，UMDF
- 添加设备 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d27e635a27db5ff1afa0d27843a8ce6aef52b8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379056"
---
# <a name="adding-a-device"></a>添加设备


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架添加驱动程序主机进程中加载每个设备的设备对象。 若要添加设备，框架将调用的驱动程序[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)方法，并传递[IWDFDriver](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver)和[IWDFDeviceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)中调用的接口。 所提供**IWDFDeviceInitialize**界面才有效驱动程序调用之前[ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)。 该驱动程序可以调用下列方法之一**IWDFDeviceInitialize**来执行以下操作：

-   驱动程序调用[ **IWDFDeviceInitialize::RetrieveDevicePropertyStore** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-retrievedevicepropertystore)方法来检索[IWDFNamedPropertyStore](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfnamedpropertystore)设备属性的接口存储区。 可以使用该驱动程序**IWDFNamedPropertyStore**用于检索和设置设备的属性。

-   驱动程序调用[ **IWDFDeviceInitialize::SetLockingConstraint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setlockingconstraint)方法，以指定框架如何调用其回调函数。

-   驱动程序调用[ **IWDFDeviceInitialize::SetFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize-setfilter)方法，以使该设备是筛选器设备。

驱动程序使用后[IWDFDeviceInitialize](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdeviceinitialize)若要初始化该设备，该驱动程序将指针传递到**IWDFDeviceInitialize**对的调用中[ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)方法来创建[UMDF 设备对象](framework-device-object.md)设备。 该驱动程序框架设备对象创建后，会调用[ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)方法来创建、 读取和写入的 I/O 队列。 在这些**IWDFDevice::CreateIoQueue**调用，该驱动程序必须确定如何从 I/O 队列接收请求。 有关详细信息，请参阅[I/O 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md)。

 

 





