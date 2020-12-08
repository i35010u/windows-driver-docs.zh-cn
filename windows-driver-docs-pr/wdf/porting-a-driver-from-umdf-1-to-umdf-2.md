---
title: 将驱动程序从 UMDF 1 移植到 UMDF 2
description: 本主题介绍如何将 User-Mode Driver Framework (UMDF) 1 驱动程序移植到 UMDF 2。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1386c606fda41ec414c599f2566da32dca2fcb1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814687"
---
# <a name="porting-a-driver-from-umdf-1-to-umdf-2"></a>将驱动程序从 UMDF 1 移植到 UMDF 2


本主题介绍如何将 User-Mode Driver Framework (UMDF) 1 驱动程序移植到 UMDF 2。 你可以从使用源/目录文件 (的 UMDF 1 驱动程序开始，而不是使用 Visual Studio 项目) ，也可以转换包含在 Visual Studio 项目中的 UMDF 1 驱动程序。 在 Visual Studio 中，结果将为 UMDF 2 驱动程序项目。 UMDF 2 驱动程序在适用于桌面版的 Windows 10 上运行， (家庭版、专业版、企业版和教育版) 以及 Windows 10 移动版。

回显驱动程序示例是已从 UMDF 1 移植到 UMDF 2 的驱动程序示例。

-   [回显示例 (UMDF 版本 1) ](https://go.microsoft.com/fwlink/p/?LinkId=617707)
-   [回显示例 (UMDF 版本 2) ](https://go.microsoft.com/fwlink/p/?LinkId=617708)

## <a name="getting-started"></a>入门


首先，在 Visual Studio 中打开新的驱动程序项目。 选择 **Visual C++- &gt; Windows 驱动程序- &gt; &gt; 用户模式驱动程序 (UMDF 2)** 模板。 Visual Studio 将打开一个部分填充的模板，其中包含驱动程序必须实现的回调函数的存根。 此新驱动程序项目将是 UMDF 2 驱动程序的基础。 使用 UMDF 2 回显示例作为你应介绍的代码类型的指南。

接下来，查看现有的 UMDF 1 驱动程序代码并确定对象映射。 UMDF 1 中的每个 COM 对象在 UMDF 2 中都有相应的 WDF 对象。 例如， **IWDFDevice** 接口映射到 WDF 设备对象，该对象由 WDFDEVICE 句柄表示。 UMDF 1 中几乎所有框架提供的接口方法在 UMDF 2 中都具有相应的方法。 例如， [**IWDFDevice：： GetDefaultIoQueue**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-getdefaultioqueue) 映射到 [**WdfDeviceGetDefaultQueue**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdefaultqueue)。

同样，驱动程序提供的回调函数在两个版本中具有等效项。 在 UMDF 1 中，驱动程序提供的接口的命名约定 (除了 **IDriverEntry**) 的 *情况* 下是对象 *回调* Xxx <strong>，而在 UMDF 2 中，驱动程序提供的例程的命名约定为 *.evt* ObjectXxx</strong>。 例如， [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 回调方法映射到 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)。

你的驱动程序在 UMDF 1 和2中都实现了回调函数，但驱动程序为其回调提供指针的方式不同。 在 UMDF 1 中，驱动程序将回调方法实现为驱动程序提供的接口的成员。 驱动程序在创建框架对象时向框架注册这些接口，例如通过调用 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)。

在 UMDF 2 中，驱动程序提供指向配置结构中驱动程序提供的回调函数的指针，如 [**WDF \_ 驱动程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config) 和 [**wdf \_ IO \_ 队列 \_ 配置**](/windows-hardware/drivers/ddi/wdfio/ns-wdfio-_wdf_io_queue_config)。

## <a name="managing-object-lifetime"></a>管理对象生存期


使用 UMDF 1 的驱动程序必须实现引用计数，以便确定何时可以安全地删除对象。 由于框架代表驱动程序跟踪对象引用，因此，UMDF 2 驱动程序无需对引用计数。

在 UMDF 2 中，每个框架对象都有一个默认的父对象。 删除父对象时，框架会删除关联的子对象。 当驱动程序调用对象创建方法（如 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)）时，它可以接受默认父级，也可以在 [**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构中指定自定义父级。 有关框架对象及其默认父对象的列表，请参阅 [框架对象的摘要](summary-of-framework-objects.md)。

## <a name="driver-initialization"></a>驱动程序初始化


UMDF 1 驱动程序实现了 [**IDriverEntry**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry) 接口。 在其 [**IDriverEntry：： OnDeviceAdd**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd) 回调方法中，驱动程序通常：

-   创建并初始化设备回调对象的实例。
-   通过调用 [**IWDFDriver：： CreateDevice**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)创建新的框架设备对象。
-   设置设备的队列及其相应的回调对象。
-   通过调用 [**IWDFDevice：： CreateDeviceInterface**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)创建设备接口类的实例。

UMDF 2 驱动程序实现 [**DriverEntry**](./driverentry-for-kmdf-drivers.md) 和 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)。 在其 **DriverEntry** 例程中，UMDF 2 驱动程序通常会调用 [**WDF \_ 驱动程序 \_ 配置 \_ INIT**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdf_driver_config_init) 来初始化驱动程序的 [**WDF \_ 驱动程序 \_ 配置**](/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config) 结构。 然后将此结构传递给 [**WdfDriverCreate**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)。

在 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 函数中，驱动程序可能会执行以下操作：

-   填写 [WDFDEVICE \_ INIT](./wdfdevice_init.md) 结构，它提供用于创建设备对象的信息。 有关使用 WDFDEVICE INIT 的详细信息 \_ ，请参阅 [创建框架设备对象](creating-a-framework-device-object.md)。
-   设置设备对象的上下文区域。 有关为框架对象分配和访问上下文空间的信息，请参阅 [框架对象上下文空间](framework-object-context-space.md)。
-   [创建设备对象](creating-a-framework-device-object.md)。
-   为设备对象指定 [请求处理程序](request-handlers.md) 。
-   [创建 i/o 队列](creating-i-o-queues.md)。
-   [创建设备接口](using-device-interfaces.md)。
-   如果设备对象拥有电源策略，请设置 [设备空闲策略](supporting-idle-power-down.md) 和 [唤醒设置](supporting-system-wake-up.md)。
-   如果硬件支持中断，则[创建中断对象](creating-an-interrupt-object.md)。

## <a name="installing-your-driver"></a>安装驱动程序


在 Visual Studio 中创建新的驱动程序项目时，新项目包含 inx 文件。 构建驱动程序时，Visual Studio 会将你的 inx 文件编译为一个 INF 文件，该文件可用作驱动程序包的一部分。

虽然 UMDF 1 驱动程序的 INF 文件必须包含驱动程序类 ID，但在 UMDF 2 驱动程序的 INF 文件中不需要 DriverCLSID。

此外，尽管 UMDF 1 驱动程序必须引用其 INF 文件中的共同安装程序，但在 UMDF 2 INF 文件中不需要 constaller 引用。 尽管 coinstaller 引用可以出现在 UMDF 2 驱动程序的 INF 文件中，但不需要一个引用。

## <a name="storing-device-context"></a>存储设备上下文


在 UMDF 1 中，驱动程序通常将设备上下文存储在驱动程序创建的回调对象中，例如通过指定设备回叫对象类的私有成员。 或者，UMDF 1 驱动程序可以调用 [**IWDFObject：： AssignContext**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-assigncontext) 方法来注册框架对象的上下文。

在 UMDF 2 中，框架根据在调用对象创建方法时驱动程序提供的可选 [**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构来分配上下文空间。 调用对象的 create 方法之后，驱动程序可以一次或多次调用 [**WdfObjectAllocateContext**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext) ，以将附加的上下文空间分配给特定的对象。 有关 UMDF 2 驱动程序应使用来定义上下文结构和访问器方法的步骤，请参阅 [框架对象上下文空间](framework-object-context-space.md)。

## <a name="debugging-your-driver"></a>调试驱动程序


若要调试 UMDF 2 驱动程序，你将使用 Wdfkd.dll 中的扩展，而不是 Wudfext.dll。 有关 Wudfext.dll 中的扩展的详细信息，请参阅 [Wdfkd.dll中的调试器扩展摘要 ](debugger-extensions-for-kmdf-drivers.md)。

在 UMDF 2 中，还可以通过即时 Trace 录像机 (IFR) 获取其他驱动程序调试信息，如在 [KMDF 和 UMDF 2 驱动程序中使用即时 Trace 录音机中](using-wpp-software-tracing-in-kmdf-and-umdf-2-drivers.md)所述。 此外，还可以使用 *框架自己的* (IFR) 。 请参阅 [使用框架的事件记录器](using-the-framework-s-event-logger.md)。

## <a name="related-topics"></a>相关主题


[UMDF 入门](getting-started-with-umdf-version-2.md)

[框架对象上下文空间](framework-object-context-space.md)

[UMDF 版本历史记录](umdf-version-history.md)

[框架对象](framework-objects.md)

 

