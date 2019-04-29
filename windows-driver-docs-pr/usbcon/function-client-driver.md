---
Description: 介绍与 USB 函数控制器扩展 (UFX) 交互时执行函数控制器客户端驱动程序的各种任务。
title: 编写函数控制器客户端驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d590b462e8898d7644737ccca9c035dfb34674c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383014"
---
# <a name="write-a-function-controller-client-driver"></a>编写函数控制器客户端驱动程序


**摘要**

-   描述函数的控制器客户端驱动程序的预期的行为。

**适用于**

-   Windows 10
-   编写 USB 设备的控制器驱动程序的驱动程序开发人员

**重要的 Api**

-   [USB 函数控制器客户端驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usb-function-controller-client-driver-reference)


介绍与 USB 函数控制器扩展 (UFX) 交互时执行函数控制器客户端驱动程序的各种任务。 UFX 和客户端驱动程序进行相互通信使用的导出方法和事件的回调函数。 导出方法 (名为**UfxDeviceXxx**或**UfxEndpointXxx**) 将由 UFX 导出并调用由客户端驱动程序。 回调函数 (名为*EVT\_UFX\_Xxx*) 将客户端驱动程序中实现并由 UFX 调用。

UFX 以异步方式调用所有客户端驱动程序的回调函数和一个回调，在每个对象的时间。 例如，是一个 USB 设备对象和三个终结点对象。 最多四个回调函数 （一个用于设备），另一个用于每个终结点可能会调用一次。 对于每个回调方法，UFX 将一直等待直到客户端驱动程序调用[ **UfxDeviceEventComplete** ](https://msdn.microsoft.com/library/windows/hardware/mt187952)以指示驱动程序已完成请求。 仅其他导出方法以等待这些导出时侦听的 UFX [ **UfxDeviceNotifyHardwareFailure**](https://msdn.microsoft.com/library/windows/hardware/mt187957)。 许多客户端回调函数是可选的。 所需的功能如下所示：

-   [*EVT\_UFX\_DEVICE\_DEFAULT\_ENDPOINT\_ADD*](https://msdn.microsoft.com/library/windows/hardware/mt187849)
-   [*EVT\_UFX\_DEVICE\_ENDPOINT\_ADD*](https://msdn.microsoft.com/library/windows/hardware/mt187851)
-   [*EVT\_UFX\_设备\_主机\_连接*](https://msdn.microsoft.com/library/windows/hardware/mt187852)
-   [*EVT\_UFX\_设备\_主机\_断开连接*](https://msdn.microsoft.com/library/windows/hardware/mt187853)
-   [*EVT\_UFX\_DEVICE\_ADDRESSED*](https://msdn.microsoft.com/library/windows/hardware/mt187847)

## <a name="initialization"></a>初始化


1.  Windows Driver Foundation (WDF) 调用的客户端驱动程序的实现时，函数的控制器客户端驱动程序启动初始化过程[ **EVT_WDF_DRIVER_DEVICE_ADD** ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调。 在该实现中，客户端驱动程序应调用[ **UfxFdoInit** ](https://msdn.microsoft.com/library/windows/hardware/mt187970) ，然后通过调用创建的设备对象[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926).
2.  客户端驱动程序调用[ **UfxDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt187951)创建 USB 设备对象并检索 UFXDEVICE 句柄。
3.  客户端驱动程序调用[ **UfxDeviceNotifyHardwareReady** ](https://msdn.microsoft.com/library/windows/hardware/mt187958)向 UFX 指示它现在可以调用客户端驱动程序的回调函数。
4.  UFX 执行初始化任务，例如：
    -   UFX 调用客户端驱动程序[ *EVT\_UFX\_设备\_默认\_终结点\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187849)实现来创建默认值终结点。
    -   UFX 创建子接口支持的设备的物理设备对象 (PDOs)。
    -   发送时将激活设备类驱动程序等待 UFX [ **IOCTL\_内部\_USBFN\_激活\_USB\_总线**](https://msdn.microsoft.com/library/windows/hardware/mt187891)请求。 它还将等待要调用的客户端驱动程序[ **UfxDeviceNotifyAttach** ](https://msdn.microsoft.com/library/windows/hardware/mt187955) ，该值指示连接设备。

## <a name="class-driver-notification"></a>类驱动程序通知


若要设置数据包和总线的状态的系统通知，类驱动程序应将发送[ **IOCTL\_内部\_USBFN\_激活\_USB\_总线**](https://msdn.microsoft.com/library/windows/hardware/mt187891)请求。 UFX 这些请求排队到类驱动程序特定的通知队列。 从客户端驱动程序收到有关总线事件的通知，UFX 从每个相应的队列中弹出，并完成请求。 若要防止从缺失的通知的类驱动程序，UFX 保持固定大小的类驱动程序的通知队列。

## <a name="device-attach-and-detach-events"></a>设备附加和分离事件


UFX 假定设备分离之前函数控制器客户端驱动程序调用[ **UfxDeviceNotifyAttach**](https://msdn.microsoft.com/library/windows/hardware/mt187955)。

该调用后 UFX 将设备状态设置为**提供支持的**USB 规范中定义。 若要通知客户端驱动程序有关状态更改，UFX 调用客户端驱动程序[ *EVT\_UFX\_设备\_USB\_状态\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187863)实现。

UFX 通知充电器驱动程序 (Cad.sys) 来帮助进行充电设备。 UFX 也会通知的类驱动程序，通过完成[ **IOCTL\_内部\_USBFN\_总线\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/mt187892)由类驱动程序以前发送的请求。

客户端驱动程序必须调用[ **UfxDeviceNotifyDetach** ](https://msdn.microsoft.com/library/windows/hardware/mt187956)分离总线时。 客户端必须仅调用一次到每次调用后分离[ **UfxDeviceNotifyAttach**](https://msdn.microsoft.com/library/windows/hardware/mt187955)。 之后**UfxDeviceNotifyDetach**调用，UFX 调用[ *EVT\_UFX\_设备\_主机\_断开连接*](https://msdn.microsoft.com/library/windows/hardware/mt187853) (如果这不是接口更改）。 UFX 然后继续执行所有清理任务，例如清除终结点的所有队列和启动默认终结点队列。 UFX 调用[ *EVT\_UFX\_设备\_USB\_状态\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187863) ，并通过完成通知的类驱动程序[**IOCTL\_内部\_USBFN\_总线\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/mt187892)请求。

**硬件故障**

如果发生硬件错误，客户端驱动程序应调用[ **UfxDeviceNotifyHardwareFailure**](https://msdn.microsoft.com/library/windows/hardware/mt187957)。 在响应中，UFX 将关闭设备堆栈，并可能会尝试通过调用客户端驱动程序从这种情况下恢复[ *EVT\_UFX\_设备\_控制器\_重置*](https://msdn.microsoft.com/library/windows/hardware/mt187848). 客户端应重置为其初始状态控制器。 如果出现另一个硬件故障，客户端应再次调用 UfxDeviceNotifyHardwareFailure。 在第二个调用时，UFX 将记录其状态和错误检查。

## <a name="port-detection"></a>端口检测


通过 UFX 执行端口检测。 它将调用函数控制器客户端驱动程序的[ *EVT\_UFX\_设备\_端口\_检测*](https://msdn.microsoft.com/library/windows/hardware/mt187855)回调函数来确定端口的类型所附加到设备。 客户端会通过调用[ **UfxDevicePortDetectComplete** ](https://msdn.microsoft.com/library/windows/hardware/mt187962)或[ **UfxDevicePortDetectCompleteEx** ](https://msdn.microsoft.com/library/windows/hardware/mt187963)其中一个端口中定义的类型[ **USBFN\_端口\_类型**](https://msdn.microsoft.com/library/windows/hardware/mt188004)。

如果客户端无法确定端口的类型，则客户端应报告**UsbfnUnknownPort**。 如果端口是未知或下游端口，则 UFX 调用客户端驱动程序[ *EVT\_UFX\_设备\_主机\_CONNECT* ](https://msdn.microsoft.com/library/windows/hardware/mt187852)函数。 UFX 侦听到总线段时间。 如果端口是未知的但没有流量，例如安装数据包时，则将假定 UFX **UsbfnStandardDownstreamPort**。 否则，UFX 分配将该端口**UsbfnInvalidDedicatedChargingPort**。 UFX 端口类型已确定后，会通知 Cad.sys 并调用客户端驱动程序[ *EVT\_UFX\_设备\_端口\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187854)函数。 该函数在客户端驱动程序是预期 ed 以更改硬件状态以匹配 UFX 端口类型。

## <a name="endpoint-creation"></a>创建终结点


UFX 通过调用客户端驱动程序创建默认终结点 （终结点 0） [ *EVT\_UFX\_设备\_默认\_终结点\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187849) ，以便它可以处理设置由主机发送的数据包。 UFX 通过调用创建其他终结点[ *EVT\_UFX\_设备\_终结点\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187851)。 UFX 仅终结点之后创建客户端驱动程序调用[ **UfxDeviceNotifyHardwareReady**](https://msdn.microsoft.com/library/windows/hardware/mt187958)。 在这些回调函数中，客户端驱动程序应调用[ **UfxEndpointCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt187965)到终结点对象，并获取其 UFXENDPOINT 句柄。 UFX 将父级设置为 PDO 关联到终结点所属的接口的类驱动程序。 默认终结点的父级是 USB 设备对象。 终结点包含两个框架队列对象： 传输队列和队列，这两种只能访问该设备处于配置状态时的命令 (除了终结点 0，可进行访问之后 UFX 调用[ *EVT\_UFX\_设备\_主机\_CONNECT*](https://msdn.microsoft.com/library/windows/hardware/mt187852))。

-   **命令队列请求**
-   [**IOCTL\_INTERNAL\_USBFN\_GET\_PIPE\_STATE**](https://msdn.microsoft.com/library/windows/hardware/mt187898)
-   [**IOCTL\_INTERNAL\_USBFN\_SET\_PIPE\_STATE**](https://msdn.microsoft.com/library/windows/hardware/mt187901)
-   [**IOCTL\_INTERNAL\_USBFN\_DESCRIPTOR\_UPDATE**](https://msdn.microsoft.com/library/windows/hardware/mt187895)
-   **传输队列请求**
-   [**IOCTL\_内部\_USBFN\_传输\_IN**](https://msdn.microsoft.com/library/windows/hardware/mt188024)
-   [**IOCTL\_内部\_USBFN\_传输\_IN\_追加\_零\_PKT**](https://msdn.microsoft.com/library/windows/hardware/mt187904)
-   [**IOCTL\_INTERNAL\_USBFN\_TRANSFER\_OUT**](https://msdn.microsoft.com/library/windows/hardware/mt187905)
-   [**IOCTL\_内部\_USBFN\_控件\_状态\_握手\_IN**](https://msdn.microsoft.com/library/windows/hardware/mt188023)
-   [**IOCTL\_内部\_USBFN\_控件\_状态\_握手\_出**](https://msdn.microsoft.com/library/windows/hardware/mt187893)

## <a name="device-enumeration"></a>设备枚举


UFX 调用的驱动程序之前，客户端驱动程序不应允许连接到主机[ *EVT\_UFX\_设备\_主机\_CONNECT*](https://msdn.microsoft.com/library/windows/hardware/mt187852)。 当客户端驱动程序调用时，设备枚举开始[ **UfxDeviceNotifyReset**](https://msdn.microsoft.com/library/windows/hardware/mt187959)。 在中**默认**状态，则 UFX 处理标准安装数据包。

**重置**

UFX 清除终结点的所有队列，并将发送[ **IOCTL\_内部\_USBFN\_描述符\_更新**](https://msdn.microsoft.com/library/windows/hardware/mt187895)更新到客户端驱动程序请求**wMaxPacketSize**的终结点 0。 UFX 启动默认终结点的队列，并将状态设置为**默认**。

**默认**

UFX 调用客户端驱动程序[ *EVT\_UFX\_设备\_USB\_状态\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187863)函数。 它还将通知类驱动程序的状态。 UFX 收到设置后\_地址标准安装数据包，UFX 将状态设置为**寻址**。

**解决**

UFX 调用客户端驱动程序[ *EVT\_UFX\_设备\_寻址*](https://msdn.microsoft.com/library/windows/hardware/mt187847)函数来指示给解决该客户端应使用。 -如果地址是 0，UFX 集状态发回**默认**并调用[ *EVT\_UFX\_设备\_USB\_状态\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187863)并通知类驱动程序。 在接收到一组\_配置标准安装数据包，UFX 将状态设置为**已配置**。

**配置**

如果所选的配置为 0，UFX 清除接口终结点，并将状态设置为**寻址**。 将发送 UFX [ **IOCTL\_内部\_USBFN\_描述符\_更新**](https://msdn.microsoft.com/library/windows/hardware/mt187895)更新到客户端驱动程序请求**wMaxPacketSize**的接口终结点。 UFX 可确保所有的接口终结点队列清除已完成并启动接口终结点队列。 如果端口类型不是**UsbfnStandardDownstreamPort**或**UsbfnChargingDownstreamPort**，UFX 将端口类型更改为**UsbfnStandardDownstreamPort** ，并通知Cad.sys;客户端驱动程序通过调用[ *EVT\_UFX\_设备\_端口\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187854)并[ *EVT\_UFX\_设备\_USB\_状态\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187863)更新的状态; 已配置状态的类驱动程序。

## <a name="standard-control-transfers"></a>标准控制传输


UFX 之后它将调用的任何时间可以处理控件上的默认终结点的传输[ *EVT\_UFX\_设备\_默认\_终结点\_添加*](https://msdn.microsoft.com/library/windows/hardware/mt187849)，在该客户端驱动程序创建默认终结点使用。 所有控制传输都开头的 8 字节安装数据包。 若要将安装程序数据包发送到主机，客户端驱动程序应调用[ **UfxEndpointNotifySetup**](https://msdn.microsoft.com/library/windows/hardware/mt187969)。 标准控制传输将完成通过 UFX。 如果使用的控制转移相关联的数据，UFX 从读取和写入相应的默认控件终结点。

## <a name="non-standard-control-transfers"></a>非标准的控制转移


如果 UFX 不能处理控制传输，传输转发到适当的类驱动程序通过完成[ **IOCTL\_内部\_USBFN\_总线\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/mt187892)请求。 控制传输可以实现任何终结点定义为终结点描述符中的控制终结点上。 非默认的控制终结点的终结点上的控制转移始终是非标准的控制转移。 如果控制终结点是默认的控制终结点，UFX 会通知标记为该类驱动程序的类请求的数据包，安装程序类驱动程序。 如果控制终结点属于一个接口，UFX 通知与该接口关联的类驱动程序。 如有必要，类驱动程序需要读取和写入到控制终结点。

## <a name="data-transfers"></a>数据传输


数据传输都由类驱动程序启动的发送[ **IOCTL\_内部\_USBFN\_传输\_IN**](https://msdn.microsoft.com/library/windows/hardware/mt188024)， [ **IOCTL\_内部\_USBFN\_传输\_IN\_追加\_零\_PKT**](https://msdn.microsoft.com/library/windows/hardware/mt187904)，或[ **IOCTL\_内部\_USBFN\_传输\_出**](https://msdn.microsoft.com/library/windows/hardware/mt187905)请求。 在验证之后的每个这些请求，UFX 将其转发到相应的终结点队列要由客户端驱动程序。 客户端驱动程序需要执行其他验证。 客户端驱动程序接收终结点队列上的传输请求。 客户端驱动程序可以检索尽可能多的请求从该队列所需以最大化总线利用率。 客户端驱动程序应完成状态为成功的请求\_成功。 该驱动程序应进行的最大努力尝试取消请求，并完成取消请求的状态\_取消如果已取消。 如果传递的参数无效，客户端驱动程序完成时具有状态的请求\_无效\_参数。

**控制传输**

控制传输开头的 8 字节安装数据包。 若要将安装程序数据包发送到主机，客户端驱动程序应调用[ **UfxEndpointNotifySetup**](https://msdn.microsoft.com/library/windows/hardware/mt187969)。 UFX 通过完成通知请求通知非标准的控制转移类驱动的程序。 使用客户端和 UFX [ **IOCTL\_内部\_USBFN\_传输\_IN**](https://msdn.microsoft.com/library/windows/hardware/mt188024)， [ **IOCTL\_内部\_USBFN\_传输\_IN\_追加\_零\_PKT**](https://msdn.microsoft.com/library/windows/hardware/mt187904)，或[ **IOCTL\_内部\_USBFN\_传输\_OUT** ](https://msdn.microsoft.com/library/windows/hardware/mt187905)以读取和写入到默认控制终结点。 但是，一个接口可定义仅相应类驱动程序可以使用其他控制终结点。 控制终结点可以安装在安装程序数据包响应。 类驱动程序发送[ **IOCTL\_内部\_USBFN\_设置\_管道\_状态**](https://msdn.microsoft.com/library/windows/hardware/mt187901)请求以停止该终结点。 硬件或客户端驱动程序被应停止发送后将立即恢复终结点上的流量。 控制终结点还可以发送和接收不包含任何以前的数据的长度为零的数据包 (ZLP)。 客户端驱动程序和 UFX 可以执行此操作通过使用[ **IOCTL\_内部\_USBFN\_控制\_状态\_握手\_IN** ](https://msdn.microsoft.com/library/windows/hardware/mt188023)并[ **IOCTL\_内部\_USBFN\_控制\_状态\_握手\_出**](https://msdn.microsoft.com/library/windows/hardware/mt187893).

**大容量和中断传输**

大容量传输保证数据传递，且用于发送大量数据。 可以在大容量终结点使用发送传输[ **IOCTL\_内部\_USBFN\_传输\_IN**](https://msdn.microsoft.com/library/windows/hardware/mt188024)， [ **IOCTL\_内部\_USBFN\_传输\_IN\_追加\_零\_PKT**](https://msdn.microsoft.com/library/windows/hardware/mt187904)，或[ **IOCTL\_内部\_USBFN\_传输\_出**](https://msdn.microsoft.com/library/windows/hardware/mt187905)。 大容量终结点可能同样停止，以控制使用的终结点[ **IOCTL\_内部\_USBFN\_设置\_管道\_状态**](https://msdn.microsoft.com/library/windows/hardware/mt187901). 客户端驱动程序应将停滞数据包发送到主机的所有请求的响应并按住 IOCTL 请求。 与不同的控制终结点已停止的大容量终结点保持已停止，直到显式清除停滞状态。

中断传输中断传输类似于大容量传输，但具有延迟保证。 中断传输具有相同的接口作为大容量传输，但不是具有流式传输功能。

**同步传输**

客户端驱动程序不应在此版本中支持同步传输。

## <a name="power-management"></a>电源管理


客户端驱动程序拥有电源管理的所有的方面。 回调函数是异步的因为预期客户端驱动程序以返回到相应的电源状态并完成请求，调用相应的事件完成导出函数，如前[ **UfxDeviceEventComplete**](https://msdn.microsoft.com/library/windows/hardware/mt187952)。

UFX 处于工作状态如果设备状态 (在中定义[ **USBFN\_设备\_状态**](https://msdn.microsoft.com/library/windows/hardware/mt187992)) 是**UsbfnDeviceStateSuspended**和**UsbfnDeviceStateAttached**，但报告端口类型。 或者，UFX 已报告的端口类型 (在中定义[ **USBFN\_端口\_类型**](https://msdn.microsoft.com/library/windows/hardware/mt188004)) **UsbfnStandardDownstreamPort**或**UsbfnChargingDownstreamPort**。

UFX 进入和退出工作状态，通过调用[ *EVT\_UFX\_设备\_USB\_状态\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187863)或[*EVT\_UFX\_设备\_端口\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187854)实现。 当客户端驱动程序调用时，转换到或从工作状态已完成[ **UfxDeviceEventComplete**](https://msdn.microsoft.com/library/windows/hardware/mt187952)。

在工作状态，UFX 可以调用任何回调。 在不工作状态下，虽然 UFX 仅调用[ *EVT\_UFX\_设备\_USB\_状态\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187863)进入工作状态;[ *EVT\_UFX\_设备\_远程\_唤醒\_信号*](https://msdn.microsoft.com/library/windows/hardware/mt187859)期间挂起 （如果发出远程唤醒支持）。

**设备挂起**

设备挂起 3 毫秒总线上没有流量时出现。 在这种情况下，客户端驱动程序必须通知 UFX 时检测到挂起和继续通过调用[ **UfxDeviceNotifySuspend** ](https://msdn.microsoft.com/library/windows/hardware/mt187961)并[ **UfxDeviceNotifyResume**](https://msdn.microsoft.com/library/windows/hardware/mt187960). 在接收这些调用，将调用 UFX [ *EVT\_UFX\_设备\_USB\_状态\_更改*](https://msdn.microsoft.com/library/windows/hardware/mt187863)和通知的类驱动程序完成[ **IOCTL\_内部\_USBFN\_总线\_事件\_通知**](https://msdn.microsoft.com/library/windows/hardware/mt187892)请求。 如果设备支持和启用由宿主远程唤醒，UFX 都可以调用调用*EVT\_UFX\_设备\_USB\_状态\_更改*挂起到问题时远程唤醒信号。

## <a name="related-topics"></a>相关主题
[在 Windows 中的 USB 设备端驱动程序](usb-device-side-drivers-in-windows.md)  
[为 USB 功能控制器开发 Windows 驱动程序](developing-windows-drivers-for-usb-function-controllers.md)  
[UFX 对象和 USB 函数客户端驱动程序使用的句柄](ufx-objects-and-handles-used-by-a-usb-function-controller.md)  



