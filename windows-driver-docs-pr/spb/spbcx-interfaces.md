---
title: SpbCx 接口
description: SPB 框架扩展 (SpbCx) 有两个接口。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f6701df555f6fb95e0cb393178a378bbb07961e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835385"
---
# <a name="spbcx-interfaces"></a>SpbCx 接口


SPB 框架扩展 (SpbCx) 有两个接口。 第一种是 i/o 请求接口，通过该接口，SpbCx 可接受 i/o 请求，客户端 (外围设备驱动程序) 的 SPB 控制器发送到连接到总线的外围设备。 第二个接口是设备驱动程序接口 (DDI) ，SpbCx 与 SPB 控制器驱动程序通信。

Spbcx 和 Spb 标头文件中定义了两个 SpbCx 接口。 Spbcx 定义 SpbCx 和 SPB 控制器驱动程序之间的 DDI。 Spb 定义 SpbCx i/o 请求接口支持的特定于 SPB 的 i/o 控制代码。

-   [SpbCx 设备驱动程序接口 (DDI) ](#spbcx-device-driver-interface-ddi)
-   [SPB i/o 请求接口](#spb-io-request-interface)

## <a name="spbcx-device-driver-interface-ddi"></a>SpbCx 设备驱动程序接口 (DDI) 


SpbCx 设备驱动程序接口 (DDI) 包含由 spb 控制器驱动程序实现的 SPB 框架扩展模块、Spbcx.sys 和事件回调函数实现的方法。 SPB 控制器驱动程序在初始化 DDI 期间将其回调函数注册到 SpbCx。

若要从 SpbCx 请求服务，则 SPB 控制器驱动程序将调用 [SpbCx 驱动程序支持方法](/previous-versions/hh450910(v=vs.85))。 例如，SPB 控制器驱动程序调用这些方法来设置 SPB 控制器的驱动程序配置选项，或获取有关 i/o 请求的其他信息。

若要通知事件 (的 SPB 控制器驱动程序，例如客户端) 发出的 i/o 请求，SpbCx 将调用由 SPB 控制器驱动程序实现的 [事件回调函数](/previous-versions/hh450911(v=vs.85)) 。

在从 SpbCx 回调期间，SPB 控制器驱动程序代码将在任意线程上下文中运行。 接收到需要由 SPB 控制器驱动程序处理的 i/o 请求后，SpbCx 会在 SpbCx 调用 *EvtSpb* Xxx 函数来执行请求的操作之前，执行请求的任何请求预处理。 例如，若要使用户模式缓冲区可用于回调函数，SpbCx 可能需要在发出 i/o 请求的线程的上下文中运行。  ([*EvtIoInCallerContext*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context) 函数是唯一不能依赖 SpbCx 来预处理请求的回调函数。 ) 

若要注册一组 *EvtSpb* Xxx 回调函数，则 SPB 控制器驱动程序将调用 [**SpbDeviceInitialize**](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbdeviceinitialize) 方法。 此驱动程序调用 [**SpbControllerSetIoOtherCallback**](/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetioothercallback) 方法来注册 *EvtIoInCallerContext* 回调函数。

SpbCx DDI 使用 WDFDEVICE 对象句柄类型来表示 SPB 控制器的设备对象。 包含 Wdf 头文件以定义 WDFDEVICE 和其他 KMDF 对象句柄类型。 此外，DDI 使用两个 SPB 特定的对象句柄类型 [**SPBREQUEST**](./spbcx-object-handles.md) 和 [**SPBTARGET**](./spbcx-object-handles.md)，它们类似于 KMDF 定义的 WDFREQUEST 和 WDFTARGET 对象句柄类型。 SPBREQUEST 句柄表示 i/o 请求。 SPBTARGET 句柄表示到总线上已为 i/o 操作打开的外围设备的逻辑连接。

简单的外围总线（如 i2c 和 SPI）通常由芯片 (SoC) 模块上的系统使用，这些端口的低 pin 计数很重要。 SoC 模块经常用作手持设备中需要低功率消耗的处理器。 因为 SPB 控制器线路消耗的电量相对较少，所以 SpbCx 中的电源管理代码可能比较简单。 默认情况下，SpbCx 确保已打开 SPB 控制器的电源，然后再调用 SPB 控制器驱动程序中的任何事件回叫方法。 有关详细信息，请参阅 [**SPB \_ 控制器 \_ CONFIG**](/windows-hardware/drivers/ddi/spbcx/ns-spbcx-_spb_controller_config)中的 **PowerManaged** 成员的说明。

如有必要，SPB 控制器驱动程序可以通过调用 [**WdfDeviceStopIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle) 和 [**WdfDeviceResumeIdle**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle) 方法显式关闭和关闭控制器的电源。

由于 SPB 控制器驱动程序是一个内核模式驱动程序，因此应为其文件对象分配适当的安全描述符。 此描述符阻止从用户模式到 SPB 上的外围设备的未经授权的访问。 例如，WDK 中的示例 SPB 控制器驱动程序使用以下 SDDL 字符串，此字符串提供适用于典型 SPB 控制器驱动程序的默认安全级别：

"D:P (A;;GA;;;SY) # B2 A;;GA;;;BA) # B4 A;;GA;;;UD) "

此 SDDL 字符串限制对操作系统 (及其用户模式组件) 、Administrators 组成员和 [用户模式驱动程序框架](../wdf/overview-of-the-umdf.md) (UMDF) 驱动程序的访问权限。 有关 SDDL 字符串的详细信息，请参阅 [适用于设备对象的 SDDL](../kernel/sddl-for-device-objects.md)。

此外， [*EvtSpbControllerIoOther*](/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_other) 函数必须验证从用户模式客户端接收的自定义 i/o 控制请求中的所有参数。 对于所有其他 *EvtSpb* Xxx 函数，SpbCx 会在将这些参数传递到 SPB 控制器驱动程序之前，验证来自用户模式客户端的 i/o 请求中的参数。 有关设备安全的详细信息，请参阅 [保护设备对象](../kernel/controlling-device-access.md)。

返回状态代码的 SpbCx DDI 中的所有方法和回调函数返回 NTSTATUS 值。 此 DDI 中的驱动程序支持方法遵循适用于 KMDF 接口的常用约定，SpbCx 使用的所有对象都遵循 KMDF 对象的常见约定。 有关详细信息，请参阅 [框架对象简介](../wdf/introduction-to-framework-objects.md)。

## <a name="spb-io-request-interface"></a>SPB i/o 请求接口


为实现 i/o 请求接口，SpbCx 管理 SPB 控制器的 i/o 队列，并监视此队列中来自 SPB 控制器的客户端的 i/o 请求。 这些客户端是用于连接到 SPB 的外围设备的用户模式和内核模式驱动程序。 应用程序无法通过 SPB i/o 请求接口直接与连接到 SPB 的外围设备通信。

SpbCx 可能会对某些 i/o 请求执行所有处理，并在将请求传递到 SPB 控制器驱动程序之前对其他请求进行预处理。 SPB 控制器驱动程序负责完成从 SpbCx 接收的请求。

客户端可以向已连接到 SPB 的外围设备发送读写请求。 为了响应 [**IRP \_ MJ \_ 读取**](/previous-versions/ff546883(v=vs.85)) 请求，SPB 控制器会将指定数量的字节从外围设备传输到客户端缓冲区。 为了响应 [**IRP \_ MJ \_ 写入**](/previous-versions/ff546904(v=vs.85)) 请求，SPB 控制器会将指定数量的字节从客户端缓冲区传输到外围设备。

除了简单的读取和写入操作外，SpbCx i/o 请求接口还支持 i/o 传输序列，这些序列合并一个或多个简单传输 (也就是说，读取和写入) 到单个原子总线操作。 在此操作过程中，会将总线专门用于传输到目标外围设备，并在操作完成之前暂时锁定总线上其他目标的访问。 SpbCx 支持 [**IOCTL \_ SPB \_ 执行 \_ 序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857) i/o 控制代码，客户端使用它来指定单个 i/o 请求中的一系列固定长度与目标设备的传输。 此 i/o 控制请求使控制器驱动程序能够优化总线传输序列以提高性能。

SpbCx i/o 请求接口支持 [**ioctl \_ spb \_ 锁定 \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858) 和 [**ioctl \_ spb \_ 解锁 \_ 控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859) I/O 控制代码，该代码用于锁定和解锁 SPB 控制器。 这些锁定和解锁请求为客户端提供了执行 i/o 传输序列的另一种方法。 在这种情况下，序列中的每个读取或写入操作由单独的读取或写入请求指定。 当客户端锁定控制器时，其他客户端将无法访问总线上的设备。 只有持有锁定的客户端才可以在总线上执行 i/o 操作。 出于此原因，客户端只应将控制器锁定一小段时间。 在传输序列完成后，客户端绝不应将控制器锁定。 有关详细信息，请参阅 [I/o 传输序列](./i-o-transfer-sequences.md)。

除了 (的 IOCTL) 代码以外，SPB 控制器驱动程序还可以支持自定义 IOCTLs。 客户端可以将 IOCTL 请求发送到代表总线上的目标设备的文件对象，这些请求到达由 SpbCx 管理的 i/o 请求队列。 如果 SpbCx 接收到一个请求，该请求包含不支持的 IOCTL 代码，则 SpbCx 会将请求直接传递到控制器驱动程序，该驱动程序将执行请求的所有处理。

SpbCx i/o 请求接口的内核模式客户端可以发送处于中断请求级别的 i/o 请求， (低 \_ 级别或调度级别的 IRQL) \_ 。 用户模式客户端只能在被动级别发送 i/o 请求 \_ 。 I/o 完成可以在被动 \_ 级别或派单级别进行 \_ 。 所有 i/o 请求都可能返回 "挂起" 状态 \_ 。

