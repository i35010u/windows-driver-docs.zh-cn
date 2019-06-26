---
title: 将驱动程序从 UMDF 1 移植到 UMDF 2
description: 本主题介绍如何移植到 UMDF 2 的用户模式驱动程序框架 (UMDF) 1 驱动程序。
ms.assetid: 99D20B4C-17C4-42AC-B4D9-F5FD64E10723
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d6c876db37ea56358e6dc85c6afc474238caae4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379667"
---
# <a name="porting-a-driver-from-umdf-1-to-umdf-2"></a>将驱动程序从 UMDF 1 移植到 UMDF 2


本主题介绍如何移植到 UMDF 2 的用户模式驱动程序框架 (UMDF) 1 驱动程序。 你可以开始使用源/目录文件 （非 Visual Studio 项目） 的 UMDF 1 驱动程序或可以转换到 Visual Studio 项目中包含的 UMDF 1 驱动程序。 结果将是 Visual Studio 中的 UMDF 2 驱动程序项目。 在桌面版本中 （主页、 专业版、 企业版和教育） 这两个 Windows 10 和 Windows 10 移动版上运行 UMDF 2 驱动程序。

Echo 驱动程序示例是为 UMDF 2 移植 UMDF 1 的驱动程序的示例。

-   [Echo 示例 （UMDF 版本 1）](https://go.microsoft.com/fwlink/p/?LinkId=617707)
-   [Echo 示例 （UMDF 版本 2）](https://go.microsoft.com/fwlink/p/?LinkId=617708)

## <a name="getting-started"></a>入门


若要开始，请在 Visual Studio 中打开一个新的驱动程序项目。 选择**可视化C++-&gt;Windows 驱动程序-&gt;WDF-&gt;用户模式驱动程序 (UMDF 2)** 模板。 Visual Studio 会打开一个部分填充的模板，包括您的驱动程序必须实现的回调函数的存根。 此新的驱动程序项目将为 UMDF 2 驱动程序的基础。 使用 UMDF 2 Echo 示例作为代码应引入的类型的指南。

接下来，查看现有 UMDF 1 驱动程序代码并确定对象映射。 UMDF 1 中的每个 COM 对象 UMDF 2 中有一个相应的 WDF 对象。 例如， **IWDFDevice**接口映射到 WDF 设备对象，表示由 WDFDEVICE 句柄。 UMDF 1 中的几乎所有框架提供的接口方法 UMDF 2 中都有对应的方法。 例如， [ **IWDFDevice::GetDefaultIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-getdefaultioqueue)映射到[ **WdfDeviceGetDefaultQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicegetdefaultqueue)。

同样，驱动程序提供的回调函数的两个版本中具有等效项。 在第 1 UMDF 驱动程序所提供的接口的命名约定 (除**IDriverEntry**) 是*我*对象*回调*Xxx<strong>，而在 UMDF 2 命名约定为驱动程序所提供的例程*Evt*ObjectXxx</strong>。 例如， [ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调方法将映射到[ *EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)。

您的驱动程序实现回调函数中 UMDF 1 和 2，但驱动程序提供指向其回调的方式有所不同。 在 UMDF 1，驱动程序为的驱动程序所提供的接口成员实现回叫方法。 该驱动程序在创建时 framework 对象，例如通过调用向框架注册这些接口[ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)。

在 UMDF 2 中，驱动程序提供了指向配置结构中的驱动程序提供的回调函数的指针等[ **WDF\_驱动程序\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)和[ **WDF\_IO\_队列\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_config)。

## <a name="managing-object-lifetime"></a>管理对象生存期


使用 UMDF 1 的驱动程序必须实现引用计数以确定何时可以安全删除的对象。 Framework 驱动程序的名义跟踪对象的引用，因为 UMDF 2 驱动程序不需要进行计数的引用。

在 UMDF 2 中，每个框架对象具有默认的父对象。 删除父对象时，框架会删除关联的子对象。 当您的驱动程序调用对象创建方法如[ **WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)，它可以接受默认的父代、 或者它可以指定中的自定义父级[ **WDF\_对象\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)结构。 Framework 对象和它们的默认父对象的列表，请参阅[Framework 对象摘要](summary-of-framework-objects.md)。

## <a name="driver-initialization"></a>驱动程序初始化


UMDF 1 驱动程序实现[ **IDriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-idriverentry)接口。 在其[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调方法，则驱动程序通常：

-   创建并初始化设备回调对象的实例。
-   通过调用创建新的 framework 设备对象[ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)。
-   设置设备的队列和其相应的回调对象。
-   通过调用创建设备接口类的实例[ **IWDFDevice::CreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)。

UMDF 2 驱动程序实现[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)并[ *EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)。 在其**DriverEntry**例程，UMDF 2 驱动程序通常会调用[ **WDF\_驱动程序\_配置\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdf_driver_config_init)初始化驱动程序的[ **WDF\_驱动程序\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构。 然后它将传递到此结构[ **WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdrivercreate)。

在其[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)函数，该驱动程序可能会执行一些以下：

-   填写[WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构，它提供用于创建设备对象的信息。 详细了解使用 WDFDEVICE\_INIT，请参阅[创建 Framework 设备对象](creating-a-framework-device-object.md)。
-   将设备对象的上下文区域设置。 有关分配和访问 framework 对象的上下文空间的信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。
-   [创建设备对象](creating-a-framework-device-object.md)。
-   指定[请求处理程序](request-handlers.md)设备对象。
-   [创建的 I/O 队列](creating-i-o-queues.md)。
-   [创建设备接口](using-device-interfaces.md)。
-   设置[设备空闲策略](supporting-idle-power-down.md)并[唤醒设置](supporting-system-wake-up.md)，如果设备对象拥有电源策略。
-   [创建中断对象](creating-an-interrupt-object.md)，如果硬件支持中断。

## <a name="installing-your-driver"></a>安装您的驱动程序


当在 Visual Studio 中创建新的驱动程序项目时，新项目将包含.inx 文件。 生成您的驱动程序时，Visual Studio 会将.inx 文件编译为可用作驱动程序包的一部分的 INF 文件。

虽然 UMDF 1 驱动程序的 INF 文件必须包含的驱动程序类 ID，则 DriverCLSID UMDF 2 驱动程序的 INF 文件中并不需要。

此外，尽管 UMDF 1 驱动程序必须引用其 INF 文件中的共同安装程序，但没有 constaller 引用需要 UMDF 2 INF 文件中。 尽管共同安装程序引用可以出现在 UMDF 2 驱动程序的 INF 文件，其中一个不需要。

## <a name="storing-device-context"></a>存储设备上下文


在 UMDF 1 中，驱动程序通常存储设备上下文中的驱动程序创建的回调对象，例如通过指定设备回调对象类的私有成员。 或者，可以调用 UMDF 1 驱动程序[ **IWDFObject::AssignContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-assigncontext)方法来注册框架对象上下文。

在 UMDF 2 中，该框架分配上下文空间根据可选[ **WDF\_对象\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)驱动程序提供了调用对象创建时的结构方法。 调用对象的 create 方法后，可以调用一个驱动程序[ **WdfObjectAllocateContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectallocatecontext)分配到特定对象的附加上下文空间的一个或多个时间。 步骤 UMDF 2 驱动程序应使用定义的上下文结构和访问器方法，请参见[框架对象上下文空间](framework-object-context-space.md)。

## <a name="debugging-your-driver"></a>调试您的驱动程序


若要调试 UMDF 2 驱动程序，您将使用中而不是 Wudfext.dll Wdfkd.dll 扩展。 有关 Wudfext.dll 中的扩展的详细信息，请参阅[摘要的调试器扩展中 Wdfkd.dll](debugger-extensions-for-kmdf-drivers.md)。

在 UMDF 2 中，您还可以获取其他驱动程序调试信息通过即时跟踪记录器 (IFR) 中，如中所述[KMDF 和 UMDF 2 驱动程序中使用即时跟踪记录器](using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)。 此外，可以使用框架的自己*正在进行录制器*(IFR)。 请参阅[使用框架的事件记录器](using-the-framework-s-event-logger.md)。

## <a name="related-topics"></a>相关主题


[UMDF 入门](getting-started-with-umdf-version-2.md)

[框架对象上下文空间](framework-object-context-space.md)

[UMDF 版本历史记录](umdf-version-history.md)

[Framework 对象](framework-objects.md)

 

 






