---
title: SpbCx 接口
description: 存储框架扩展 (SpbCx) 有两个接口。
ms.assetid: 2449BB88-1912-43F9-97E6-B56158D92E55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774fa08bc5ad47325732488524df68ee5d2a06f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543914"
---
# <a name="spbcx-interfaces"></a>SpbCx 接口


存储框架扩展 (SpbCx) 有两个接口。 首先，通过该 SpbCx 接受 I/O 请求的存储控制器的客户端 （外围设备驱动程序） 发送到连接到总线的外围设备的 I/O 请求接口。 第二个接口是通过其 SpbCx 与存储控制器驱动程序进行通信的设备驱动程序接口 (DDI)。

Spbcx.h 和 Spb.h 标头文件中定义的两个 SpbCx 接口。 Spbcx.h 定义 DDI SpbCx 和存储控制器驱动程序之间。 Spb.h 定义受 SpbCx I/O 请求接口的特定于存储的 I/O 控制代码。

-   [SpbCx 设备驱动程序接口 (DDI)](#spbcx-device-driver-interface-ddi)
-   [存储 I/O 请求接口](#spb-io-request-interface)

## <a name="spbcx-device-driver-interface-ddi"></a>SpbCx 设备驱动程序接口 (DDI)


SpbCx 设备驱动程序接口 (DDI) 包含的存储 framework 扩展模块、 Spbcx.sys 和事件回调函数的存储控制器驱动程序实现所实现方法。 存储控制器驱动程序注册其回调函数 SpbCx DDI 的初始化过程。

从 SpbCx，存储控制器驱动程序调用的请求服务[SpbCx 驱动程序支持的方法](https://msdn.microsoft.com/library/windows/hardware/hh450910)。 例如，存储控制器驱动程序调用这些方法可以设置的存储控制器驱动程序配置选项或要获得有关的 I/O 请求的其他信息。

若要通知的事件 （例如，到达的 I/O 请求从客户端） 的存储控制器驱动程序调用 SpbCx[事件的回调函数](https://msdn.microsoft.com/library/windows/hardware/hh450911)实现的存储控制器驱动程序。

在从 SpbCx 回调，期间存储控制器驱动程序代码在任意线程上下文中运行。 收到存储控制器驱动程序需要处理 I/O 请求后，SpbCx 是否任何所需的 SpbCx 调用之前请求的预处理*EvtSpb*Xxx 函数来执行请求的操作。 例如，若要将用户模式缓冲区提供给回调函数，SpbCx 可能需要在发起 I/O 请求的线程上下文中运行。 ( [ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764)函数是不能依赖于 SpbCx 进行预处理请求的唯一的回调函数。)

若要注册一套*EvtSpb*Xxx 回调函数的存储控制器驱动程序调用[ **SpbDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/hh450919)方法。 此驱动程序调用[ **SpbControllerSetIoOtherCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh450907)方法来注册*EvtIoInCallerContext*回调函数。

SpbCx DDI 使用 WDFDEVICE 对象句柄类型来表示存储控制器的设备对象。 包括 Wdf.h 标头文件以定义 WDFDEVICE 和其他 KMDF 对象句柄类型。 此外，DDI 使用两个特定于存储的对象句柄类型[ **SPBREQUEST** ](https://msdn.microsoft.com/library/windows/hardware/hh450925)并[ **SPBTARGET**](https://msdn.microsoft.com/library/windows/hardware/hh406201)，这是类似于WDFREQUEST 和 WDFTARGET 对象处理通过 KMDF 定义的类型。 SPBREQUEST 句柄表示的 I/O 请求。 SPBTARGET 句柄表示的逻辑连接到外围设备已打开总线上的 I/O 操作。

简单的外围总线如 I²C 和 SPI 通常由系统上使用芯片 (SoC) 模块的低 pin 计数是很重要。 SoC 模块经常用作在要求较低的功率消耗的手持设备的处理器。 由于存储控制器线路占用相对较少的功率，SpbCx 中的电源管理代码可以变得相对简单。 默认情况下，SpbCx 可确保存储控制器的电源已打开之前它调用任何事件回叫方法中的存储控制器驱动程序。 有关详细信息，请参阅的说明**PowerManaged**中的成员[**存储\_控制器\_配置**](https://msdn.microsoft.com/library/windows/hardware/hh406206)。

如果有必要，存储控制器驱动程序可以显式打开为打开和关闭控制器通过调用[ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)并[ **WdfDeviceResumeIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546838)方法。

由于存储控制器驱动程序的内核模式驱动程序，它应将适当的安全描述符分配给其文件对象。 此说明符可防止未经授权的访问用户模式下从存储中的外围设备。 例如，在 WDK 中的示例存储控制器驱动程序使用提供的适用于典型的存储控制器驱动程序的安全默认级别的以下 SDDL 字符串：

"D:P(A;;GA;;;SY)(A;;GA;;;BA)(A;;GA;;;UD)"

此 SDDL 字符串限制访问权限的操作系统 （和其用户模式组件），管理员组的成员以及[用户模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff560442)(UMDF) 驱动程序。 有关 SDDL 字符串的详细信息，请参阅[设备对象的 SDDL](https://msdn.microsoft.com/library/windows/hardware/ff563667)。

此外， [ *EvtSpbControllerIoOther* ](https://msdn.microsoft.com/library/windows/hardware/hh450805)函数必须验证自定义它从用户模式下客户端接收的 I/O 控制请求中的所有参数。 对于所有其他*EvtSpb*Xxx 函数，这些参数传递到存储控制器驱动程序之前 SpbCx 验证来自用户模式下客户端的 I/O 请求中的参数。 有关设备安全性的详细信息，请参阅[保护设备对象](https://msdn.microsoft.com/library/windows/hardware/ff563688)。

所有方法和 SpbCx DDI 中的回调函数，都返回状态代码都返回 NTSTATUS 值。 此 DDI 中的驱动程序支持方法遵循的常见约定对于 KMDF 接口，并由 SpbCx 的所有对象都按照 KMDF 对象的常用规则。 有关详细信息，请参阅[Framework 对象简介](https://msdn.microsoft.com/library/windows/hardware/ff544249)。

## <a name="spb-io-request-interface"></a>存储 I/O 请求接口


若要实现的 I/O 请求接口，SpbCx 管理存储控制器的 I/O 队列，并监视此队列的存储控制器的客户端的 I/O 请求。 这些客户端是连接到存储的外围设备的用户模式和内核模式驱动程序。 应用程序不能直接与存储连接的外围设备通过存储 I/O 请求接口通信。

SpbCx 可能对其进行某些这些 I/O 请求，所有处理和执行都操作的其他请求的预处理才能将请求传递给存储控制器驱动程序。 存储控制器驱动程序负责完成 SpbCx 从其接收的请求。

客户端可以发送读取和写入请求发送到已连接存储的外围设备。 以响应[ **IRP\_MJ\_读取**](https://msdn.microsoft.com/library/windows/hardware/ff546883)请求，存储控制器将指定的字节数从外围设备传输到客户端缓冲区。 以响应[ **IRP\_MJ\_编写**](https://msdn.microsoft.com/library/windows/hardware/ff546904)请求，存储控制器将指定的字节数从客户端缓冲区传输到外围设备。

除了简单的读取和写入操作，SpbCx I/O 请求接口还支持 I/O 传输序列，这将合并一个或多个简单传输 （的是，读取和写入） 到单一的原子总线操作。 此操作期间总线专门用于接收和从目标外围设备，并访问总线上的其他目标被暂时锁定在操作完成之前。 支持 SpbCx [ **IOCTL\_存储\_EXECUTE\_序列**](https://msdn.microsoft.com/library/windows/hardware/hh450857) I/O 控制代码，客户端使用与指定的固定长度传输序列单个的 I/O 请求中的目标设备。 此 I/O 控制请求，控制器驱动程序来优化一系列总线传输来提高性能。

SpbCx I/O 请求接口支持[ **IOCTL\_存储\_锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450858)并[ **IOCTL\_存储\_解锁\_控制器**](https://msdn.microsoft.com/library/windows/hardware/hh450859) I/O 控制代码，这些锁定和解锁存储控制器的代码。 这些锁定和解锁请求提供客户端来执行 I/O 传输序列的另一种方法。 在这种情况下，每个读或写操作的顺序指定的单独读取或写入请求。 虽然客户端具有已锁定的控制器，其他客户端无法访问总线上的设备。 持有锁的客户端可以执行总线上的 I/O 操作。 出于此原因，客户端应仅为在短时间内锁定控制器。 客户端绝不会脱离锁定传输序列完成后的控制器。 有关详细信息，请参阅[I/O 传输序列](https://msdn.microsoft.com/library/windows/hardware/hh450890)。

支持的 SpbCx 的 I/O 控制 (IOCTL) 代码，除了存储控制器驱动程序可以支持自定义 Ioctl。 客户端可以将 IOCTL 请求发送到代表在总线上的目标设备的文件对象，并且这些请求由 SpbCx 在 I/O 请求队列中。 如果 SpbCx 收到的请求的不支持一个 IOCTL 代码，SpbCx 请求将直接传递到控制器驱动程序，可以执行所有处理请求。

内核模式下客户端的 SpbCx I/O 操作的请求接口可以将 I/O 请求发送中断请求 (IRQL) 的级别是被动\_级别或调度\_级别。 用户模式下客户端可以发送的 I/O 请求，仅在被动\_级别。 I/O 完成可以出现在被动\_级别或调度\_级别。 所有 I/O 请求可以都返回状态\_PENDING。

 

 




