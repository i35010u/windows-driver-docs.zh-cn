---
title: 在 UMDF 驱动程序中使用设备接口
description: 在 UMDF 驱动程序中使用设备接口
ms.assetid: acb6da80-bd04-48f0-b42a-96463f091b0a
keywords:
- 用户模式驱动程序 WDK UMDF，设备接口
- UMDF WDK，设备接口
- 用户模式驱动程序框架 WDK，设备接口
- 设备接口 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e882d43204ffae3e77ff51c4d40dea24c8e0b2b
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242872"
---
# <a name="using-device-interfaces-in-umdf-drivers"></a>在 UMDF 驱动程序中使用设备接口


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

*设备接口*是应用程序可用于访问设备的即插即用（PnP）设备的符号链接。 用户模式应用程序可将接口的符号链接名称传递到 API 元素，例如 Microsoft Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数。 若要获取设备接口的符号链接名称，用户模式应用程序可以调用**SetupDi**函数。 有关 SetupDi 函数的详细信息，请参阅 SetupDi 设备接口函数。

每个设备接口属于一个*设备接口类*。 例如，cd-rom 设备的驱动程序堆栈可能会提供属于 GUID\_DEVINTERFACE\_CDROM 类的接口。 CD-ROM 设备的驱动程序之一会将 GUID 的实例注册\_DEVINTERFACE\_CDROM 类，以便向系统和应用程序提供 CD-ROM 设备。 有关设备接口类的详细信息，请参阅[设备接口简介](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)。

### <a name="registering-a-device-interface"></a>注册设备接口

若要注册设备接口类的实例，基于 UMDF 的驱动程序可以从其[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调函数中调用[**IWDFDevice：： CreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface) 。 如果驱动程序支持多个接口实例，则可以为每个实例分配一个唯一的引用字符串。

### <a name="enabling-and-disabling-a-device-interface"></a>启用和禁用设备接口

如果创建成功，则框架将基于设备的 PnP 状态自动启用和禁用接口。

此外，驱动程序还可以根据需要禁用和重新启用设备接口。 例如，如果驱动程序确定其设备已停止响应，则驱动程序可以调用[**IWDFDevice：： AssignDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-assigndeviceinterfacestate)来禁用设备的接口，并禁止应用程序获取接口的新句柄。 （接口的现有句柄不受影响。）如果该设备稍后变为可用，则驱动程序可以再次调用**IWDFDevice：： AssignDeviceInterfaceState**来重新启用接口。

### <a name="receiving-requests-to-access-a-device-interface"></a>接收访问设备接口的请求

当应用程序请求访问驱动程序的设备接口时，框架会调用驱动程序的[**IQueueCallbackCreate：： OnCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)回调函数。 驱动程序可以调用[**IWDFFile：： RetrieveFileName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffile-retrievefilename)以获取应用程序正在访问的设备或文件的名称。 如果驱动程序在注册设备接口时指定了引用字符串，则操作系统会在**IWDFFile：： RetrieveFileName**返回的文件或设备名称中包含引用字符串。

### <a name="creating-device-events"></a>创建设备事件

基于 UMDF 的驱动程序可以通过调用 IWDFDevice 来创建设备特定的自定义事件（称为*设备事件*） [ **：:P ostevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-postevent)。 已注册为使用任何设备接口的驱动程序可以接收设备自定义事件的通知。 基于 UMDF 的驱动程序通过提供[**IRemoteInterfaceCallbackEvent：： OnRemoteInterfaceEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremoteinterfacecallbackevent-onremoteinterfaceevent)回调函数来接收此类通知。

自定义事件对于设备是唯一的。 创建事件的驱动程序开发人员和接收事件的驱动程序的开发人员必须了解事件的含义。

### <a name="accessing-another-drivers-device-interface"></a>访问另一个驱动程序的设备接口

如果希望基于 UMDF 的驱动程序将 i/o 请求发送到另一个驱动程序提供的设备接口，则可以创建表示设备接口的[远程 i/o 目标](general-i-o-targets-in-umdf.md)。

首先，你的驱动程序必须注册，以便在设备接口可用时接收通知。 请使用以下步骤：

1.  当驱动程序调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)时，驱动程序可以提供一个[IPnpCallbackRemoteInterfaceNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackremoteinterfacenotification)接口。 当设备接口可用时，此接口的[**IPnpCallbackRemoteInterfaceNotification：： OnRemoteInterfaceArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)回调函数会通知你的驱动程序。

2.  驱动程序调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)后，它可为驱动程序将使用的每个设备接口调用[**IWDFDevice2：： RegisterRemoteInterfaceNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-registerremoteinterfacenotification) 。

然后，每当指定的设备接口可用时，框架都会调用驱动程序的[**IPnpCallbackRemoteInterfaceNotification：： OnRemoteInterfaceArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)回调函数。 回调函数可以调用[**IWDFRemoteInterfaceInitialize：： GetInterfaceGuid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremoteinterfaceinitialize-getinterfaceguid)和[**IWDFRemoteInterfaceInitialize：： RetrieveSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremoteinterfaceinitialize-retrievesymboliclink)来确定已到达哪个设备接口。

驱动程序的[**IPnpCallbackRemoteInterfaceNotification：： OnRemoteInterfaceArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)回调函数通常应执行以下操作：

1.  调用[**IWDFDevice2：： CreateRemoteInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-createremoteinterface)以创建远程接口对象，可选择提供[IRemoteInterfaceCallbackEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremoteinterfacecallbackevent)和[IRemoteInterfaceCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremoteinterfacecallbackremoval)接口。

2.  调用[**IWDFDevice2：： CreateRemoteTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-createremotetarget)以创建远程目标对象，可选择提供[IRemoteTargetCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iremotetargetcallbackremoval)接口。

3.  调用[**IWDFRemoteTarget：： OpenRemoteInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface)将设备接口连接到远程目标。

    如果设备接口是 SWENUM software 设备枚举器创建的接口，则驱动程序必须从工作项调用**OpenRemoteInterface** 。 （有关示例，请参阅 Windows SDK 中的**QueueUserWorkItem**函数。）

现在，驱动程序可以格式化 i/o 请求并将其发送到远程 i/o 目标。

除了[**IPnpCallbackRemoteInterfaceNotification：： OnRemoteInterfaceArrival**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)回调函数外，基于 UMDF 的驱动程序还可以提供两个额外的回调函数来接收设备接口事件的通知：

-   删除设备接口后， [**IRemoteInterfaceCallbackRemoval：： OnRemoteInterfaceRemoval**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremoteinterfacecallbackremoval-onremoteinterfaceremoval)回调函数会通知驱动程序。

-   当设备的自定义事件到达时， [**IRemoteInterfaceCallbackEvent：： OnRemoteInterfaceEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iremoteinterfacecallbackevent-onremoteinterfaceevent)回调函数通知驱动程序。

 

 





