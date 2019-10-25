---
title: 将驱动程序从 UMDF 1 移植到 UMDF 2
description: 本主题介绍如何将用户模式驱动程序框架（UMDF）1驱动程序移植到 UMDF 2。
ms.assetid: 99D20B4C-17C4-42AC-B4D9-F5FD64E10723
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36c9231ab2c56167c2f2b245dfecc990ea812bab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827247"
---
# <a name="porting-a-driver-from-umdf-1-to-umdf-2"></a>将驱动程序从 UMDF 1 移植到 UMDF 2


本主题介绍如何将用户模式驱动程序框架（UMDF）1驱动程序移植到 UMDF 2。 你可以从使用源/目录文件（而不是 Visual Studio 项目）的 UMDF 1 驱动程序开始，或者转换包含在 Visual Studio 项目中的 UMDF 1 驱动程序。 在 Visual Studio 中，结果将为 UMDF 2 驱动程序项目。 UMDF 2 驱动程序在适用于桌面版的 Windows 10 （家庭版、专业版、企业版和教育版）和 Windows 10 移动版上运行。

回显驱动程序示例是已从 UMDF 1 移植到 UMDF 2 的驱动程序示例。

-   [回显示例（UMDF 版本1）](https://go.microsoft.com/fwlink/p/?LinkId=617707)
-   [回显示例（UMDF 版本2）](https://go.microsoft.com/fwlink/p/?LinkId=617708)

## <a name="getting-started"></a>入门


首先，在 Visual Studio 中打开新的驱动程序项目。 选择 **&gt;Windows 驱动程序&gt;WDF-&gt;用户模式驱动程序（UMDF 2）模板。 C++** Visual Studio 将打开一个部分填充的模板，其中包含驱动程序必须实现的回调函数的存根。 此新驱动程序项目将是 UMDF 2 驱动程序的基础。 使用 UMDF 2 回显示例作为你应介绍的代码类型的指南。

接下来，查看现有的 UMDF 1 驱动程序代码并确定对象映射。 UMDF 1 中的每个 COM 对象在 UMDF 2 中都有相应的 WDF 对象。 例如， **IWDFDevice**接口映射到 WDF 设备对象，该对象由 WDFDEVICE 句柄表示。 UMDF 1 中几乎所有框架提供的接口方法在 UMDF 2 中都具有相应的方法。 例如， [**IWDFDevice：： GetDefaultIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-getdefaultioqueue)映射到[**WdfDeviceGetDefaultQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdefaultqueue)。

同样，驱动程序提供的回调函数在两个版本中具有等效项。 在 UMDF 1 中，驱动程序提供的接口（ **IDriverEntry**除外）的命名约定为*I*Object*回*Xxx<strong>，而在 UMDF 2 中，驱动程序提供的例程的命名约定为 *.evt*ObjectXxx</strong>。 例如， [**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调方法映射到[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)。

你的驱动程序在 UMDF 1 和2中都实现了回调函数，但驱动程序为其回调提供指针的方式不同。 在 UMDF 1 中，驱动程序将回调方法实现为驱动程序提供的接口的成员。 驱动程序在创建框架对象时向框架注册这些接口，例如通过调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)。

在 UMDF 2 中，驱动程序在配置结构中提供了驱动程序提供的回调函数的指针，如[**WDF\_驱动程序\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)和[**wdf\_IO\_队列\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)。

## <a name="managing-object-lifetime"></a>管理对象生存期


使用 UMDF 1 的驱动程序必须实现引用计数，以便确定何时可以安全地删除对象。 由于框架代表驱动程序跟踪对象引用，因此，UMDF 2 驱动程序无需对引用计数。

在 UMDF 2 中，每个框架对象都有一个默认的父对象。 删除父对象时，框架会删除关联的子对象。 当驱动程序调用对象创建方法（如[**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)）时，它可以接受默认父级，也可以在[**WDF\_对象\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构中指定自定义父级。 有关框架对象及其默认父对象的列表，请参阅[框架对象的摘要](summary-of-framework-objects.md)。

## <a name="driver-initialization"></a>驱动程序初始化


UMDF 1 驱动程序实现了[**IDriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry)接口。 在其[**IDriverEntry：： OnDeviceAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调方法中，驱动程序通常：

-   创建并初始化设备回调对象的实例。
-   通过调用[**IWDFDriver：： CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)创建新的框架设备对象。
-   设置设备的队列及其相应的回调对象。
-   通过调用[**IWDFDevice：： CreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)创建设备接口类的实例。

UMDF 2 驱动程序实现[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)和[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)。 在其**DriverEntry**例程中，UMDF 2 驱动程序通常[ **\_config\_INIT 调用 WDF\_驱动**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdf_driver_config_init)程序，以初始化驱动程序的[**WDF\_驱动程序\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)结构。 然后将此结构传递给[**WdfDriverCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)。

在[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)函数中，驱动程序可能会执行以下操作：

-   填写[WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)结构，它提供用于创建设备对象的信息。 有关使用 WDFDEVICE\_INIT 的详细信息，请参阅[创建框架设备对象](creating-a-framework-device-object.md)。
-   设置设备对象的上下文区域。 有关为框架对象分配和访问上下文空间的信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。
-   [创建设备对象](creating-a-framework-device-object.md)。
-   为设备对象指定[请求处理程序](request-handlers.md)。
-   [创建 i/o 队列](creating-i-o-queues.md)。
-   [创建设备接口](using-device-interfaces.md)。
-   如果设备对象拥有电源策略，请设置[设备空闲策略](supporting-idle-power-down.md)和[唤醒设置](supporting-system-wake-up.md)。
-   如果硬件支持中断，则[创建中断对象](creating-an-interrupt-object.md)。

## <a name="installing-your-driver"></a>安装驱动程序


在 Visual Studio 中创建新的驱动程序项目时，新项目包含 inx 文件。 构建驱动程序时，Visual Studio 会将你的 inx 文件编译为一个 INF 文件，该文件可用作驱动程序包的一部分。

虽然 UMDF 1 驱动程序的 INF 文件必须包含驱动程序类 ID，但在 UMDF 2 驱动程序的 INF 文件中不需要 DriverCLSID。

此外，尽管 UMDF 1 驱动程序必须引用其 INF 文件中的共同安装程序，但在 UMDF 2 INF 文件中不需要 constaller 引用。 尽管 coinstaller 引用可以出现在 UMDF 2 驱动程序的 INF 文件中，但不需要一个引用。

## <a name="storing-device-context"></a>存储设备上下文


在 UMDF 1 中，驱动程序通常将设备上下文存储在驱动程序创建的回调对象中，例如通过指定设备回叫对象类的私有成员。 或者，UMDF 1 驱动程序可以调用[**IWDFObject：： AssignContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext)方法来注册框架对象的上下文。

在 UMDF 2 中，框架根据可选的 WDF\_对象分配上下文空间，该[**对象\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)结构，当驱动程序调用对象创建方法时，驱动程序提供此结构。 调用对象的 create 方法之后，驱动程序可以一次或多次调用[**WdfObjectAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext) ，以将附加的上下文空间分配给特定的对象。 有关 UMDF 2 驱动程序应使用来定义上下文结构和访问器方法的步骤，请参阅[框架对象上下文空间](framework-object-context-space.md)。

## <a name="debugging-your-driver"></a>调试驱动程序


若要调试 UMDF 2 驱动程序，你将使用 Wdfkd 中的扩展，而不是 Wudfext。 有关 Wudfext 中的扩展的详细信息，请参阅[Wdfkd 中的调试器扩展摘要](debugger-extensions-for-kmdf-drivers.md)。

在 UMDF 2 中，还可以通过即时 Trace 录像机（IFR）获取其他驱动程序调试信息，如[使用 KMDF 和 UMDF 2 驱动程序中的即时 Trace 录音机中](using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)所述。 此外，还可以使用框架自己的*正在进行的记录器*（IFR）。 请参阅[使用框架的事件记录器](using-the-framework-s-event-logger.md)。

## <a name="related-topics"></a>相关主题


[UMDF 入门](getting-started-with-umdf-version-2.md)

[框架对象上下文空间](framework-object-context-space.md)

[UMDF 版本历史记录](umdf-version-history.md)

[框架对象](framework-objects.md)

 

 






