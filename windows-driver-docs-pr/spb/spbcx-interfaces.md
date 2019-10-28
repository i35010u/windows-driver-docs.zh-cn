---
title: SpbCx 接口
description: SPB 框架扩展（SpbCx）具有两个接口。
ms.assetid: 2449BB88-1912-43F9-97E6-B56158D92E55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 857ed210558c1da8bc1b20879b43aa1f2c5139ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839626"
---
# <a name="spbcx-interfaces"></a>SpbCx 接口


SPB 框架扩展（SpbCx）具有两个接口。 第一种是 i/o 请求接口，SpbCx 可通过此接口接受 SPB 控制器的客户端（外设驱动程序）发送到连接到总线的外围设备的 i/o 请求。 第二个接口是设备驱动程序接口（DDI），SpbCx 与 SPB 控制器驱动程序通信。

Spbcx 和 Spb 标头文件中定义了两个 SpbCx 接口。 Spbcx 定义 SpbCx 和 SPB 控制器驱动程序之间的 DDI。 Spb 定义 SpbCx i/o 请求接口支持的特定于 SPB 的 i/o 控制代码。

-   [SpbCx 设备驱动程序接口（DDI）](#spbcx-device-driver-interface-ddi)
-   [SPB i/o 请求接口](#spb-io-request-interface)

## <a name="spbcx-device-driver-interface-ddi"></a>SpbCx 设备驱动程序接口（DDI）


SpbCx 设备驱动程序接口（DDI）包含由 spb 控制器驱动程序实现的 SPB 框架扩展模块、Spbcx 和事件回调函数实现的方法。 SPB 控制器驱动程序在初始化 DDI 期间将其回调函数注册到 SpbCx。

若要从 SpbCx 请求服务，则 SPB 控制器驱动程序将调用[SpbCx 驱动程序支持方法](https://docs.microsoft.com/previous-versions/hh450910(v=vs.85))。 例如，SPB 控制器驱动程序调用这些方法来设置 SPB 控制器的驱动程序配置选项，或获取有关 i/o 请求的其他信息。

若要通知事件的 SPB 控制器驱动程序（例如，来自客户端的 i/o 请求到达），SpbCx 将调用由 SPB 控制器驱动程序实现的[事件回调函数](https://docs.microsoft.com/previous-versions/hh450911(v=vs.85))。

在从 SpbCx 回调期间，SPB 控制器驱动程序代码将在任意线程上下文中运行。 接收到需要由 SPB 控制器驱动程序处理的 i/o 请求后，SpbCx 会在 SpbCx 调用*EvtSpb*Xxx 函数来执行请求的操作之前，执行请求的任何请求预处理。 例如，若要使用户模式缓冲区可用于回调函数，SpbCx 可能需要在发出 i/o 请求的线程的上下文中运行。 （ [*EvtIoInCallerContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)函数是唯一不能依赖 SpbCx 来预处理请求的回调函数。）

若要注册一组*EvtSpb*Xxx 回调函数，则 SPB 控制器驱动程序将调用[**SpbDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbdeviceinitialize)方法。 此驱动程序调用[**SpbControllerSetIoOtherCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetioothercallback)方法来注册*EvtIoInCallerContext*回调函数。

SpbCx DDI 使用 WDFDEVICE 对象句柄类型来表示 SPB 控制器的设备对象。 包含 Wdf 头文件以定义 WDFDEVICE 和其他 KMDF 对象句柄类型。 此外，DDI 使用两个 SPB 特定的对象句柄类型[**SPBREQUEST**](https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-object-handles)和[**SPBTARGET**](https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-object-handles)，它们类似于 KMDF 定义的 WDFREQUEST 和 WDFTARGET 对象句柄类型。 SPBREQUEST 句柄表示 i/o 请求。 SPBTARGET 句柄表示到总线上已为 i/o 操作打开的外围设备的逻辑连接。

简单的外围总线（如 i2c 和 SPI）通常由芯片（SoC）模块上的系统使用，这些端口的低 pin 计数很重要。 SoC 模块经常用作手持设备中需要低功率消耗的处理器。 因为 SPB 控制器线路消耗的电量相对较少，所以 SpbCx 中的电源管理代码可能比较简单。 默认情况下，SpbCx 确保已打开 SPB 控制器的电源，然后再调用 SPB 控制器驱动程序中的任何事件回叫方法。 有关详细信息，请参阅 SPB 中**PowerManaged**成员的说明[ **\_控制器\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/ns-spbcx-_spb_controller_config)。

如有必要，SPB 控制器驱动程序可以通过调用[**WdfDeviceStopIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)和[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)方法显式关闭和关闭控制器的电源。

由于 SPB 控制器驱动程序是一个内核模式驱动程序，因此应为其文件对象分配适当的安全描述符。 此描述符阻止从用户模式到 SPB 上的外围设备的未经授权的访问。 例如，WDK 中的示例 SPB 控制器驱动程序使用以下 SDDL 字符串，此字符串提供适用于典型 SPB 控制器驱动程序的默认安全级别：

"D:P （A;;GA;;;SY）（A;;GA;;;BA）（A;;GA;;;UD） "

此 SDDL 字符串限制对操作系统（及其用户模式组件）、Administrators 组成员和[用户模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)（UMDF）驱动程序的访问。 有关 SDDL 字符串的详细信息，请参阅[适用于设备对象的 SDDL](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)。

此外， [*EvtSpbControllerIoOther*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_other)函数必须验证从用户模式客户端接收的自定义 i/o 控制请求中的所有参数。 对于所有其他*EvtSpb*Xxx 函数，SpbCx 会在将这些参数传递到 SPB 控制器驱动程序之前，验证来自用户模式客户端的 i/o 请求中的参数。 有关设备安全的详细信息，请参阅[保护设备对象](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)。

返回状态代码的 SpbCx DDI 中的所有方法和回调函数返回 NTSTATUS 值。 此 DDI 中的驱动程序支持方法遵循适用于 KMDF 接口的常用约定，SpbCx 使用的所有对象都遵循 KMDF 对象的常见约定。 有关详细信息，请参阅[框架对象简介](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)。

## <a name="spb-io-request-interface"></a>SPB i/o 请求接口


为实现 i/o 请求接口，SpbCx 管理 SPB 控制器的 i/o 队列，并监视此队列中来自 SPB 控制器的客户端的 i/o 请求。 这些客户端是用于连接到 SPB 的外围设备的用户模式和内核模式驱动程序。 应用程序无法通过 SPB i/o 请求接口直接与连接到 SPB 的外围设备通信。

SpbCx 可能会对某些 i/o 请求执行所有处理，并在将请求传递到 SPB 控制器驱动程序之前对其他请求进行预处理。 SPB 控制器驱动程序负责完成从 SpbCx 接收的请求。

客户端可以向已连接到 SPB 的外围设备发送读写请求。 为了响应[**IRP\_MJ\_读取**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))请求，SPB 控制器将指定数量的字节从外围设备传输到客户端缓冲区。 为了响应[**IRP\_MJ\_写入**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))请求，SPB 控制器会将指定数量的字节从客户端缓冲区传输到外围设备。

除了简单的读取和写入操作外，SpbCx i/o 请求接口还支持 i/o 传输序列，将一个或多个简单传输（即，读取和写入）合并为一个原子总线操作。 在此操作过程中，会将总线专门用于传输到目标外围设备，并在操作完成之前暂时锁定总线上其他目标的访问。 SpbCx 支持[**IOCTL\_SPB\_执行\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857)i/o 控制代码，客户端使用此控制代码在单个 i/o 请求中指定与目标设备的固定长度的传输顺序。 此 i/o 控制请求使控制器驱动程序能够优化总线传输序列以提高性能。

SpbCx i/o 请求接口支持[**IOCTL\_spb\_锁定\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858)和[**ioctl\_SPB\_解锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859)i/o 控制代码，这会锁定和解除对 SPB 控制器的锁定。 这些锁定和解锁请求为客户端提供了执行 i/o 传输序列的另一种方法。 在这种情况下，序列中的每个读取或写入操作由单独的读取或写入请求指定。 当客户端锁定控制器时，其他客户端将无法访问总线上的设备。 只有持有锁定的客户端才可以在总线上执行 i/o 操作。 出于此原因，客户端只应将控制器锁定一小段时间。 在传输序列完成后，客户端绝不应将控制器锁定。 有关详细信息，请参阅[I/o 传输序列](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)。

除了 SpbCx 支持的 i/o 控制（IOCTL）代码外，SPB 控制器驱动程序还可以支持自定义 IOCTLs。 客户端可以将 IOCTL 请求发送到代表总线上的目标设备的文件对象，这些请求到达由 SpbCx 管理的 i/o 请求队列。 如果 SpbCx 接收到一个请求，该请求包含不支持的 IOCTL 代码，则 SpbCx 会将请求直接传递到控制器驱动程序，该驱动程序将执行请求的所有处理。

SpbCx i/o 请求接口的内核模式客户端可以发送 i/o 请求，其中断请求级别（IRQL）为被动\_级别或调度\_级别。 用户模式客户端只能在被动\_级别发送 i/o 请求。 I/o 完成可以在被动\_级别或调度\_级别进行。 所有 i/o 请求都可能返回状态\_"挂起"。

 

 




