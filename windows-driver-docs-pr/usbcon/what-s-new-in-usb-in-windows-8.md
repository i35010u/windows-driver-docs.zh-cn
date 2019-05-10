---
Description: 本主题总结了新功能和 Windows 8 中的通用串行总线 (USB) 客户端驱动程序的改进。
title: Windows 8-什么是 USB 的新增功能
ms.date: 05/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 252462c9f33b45dc6155595776366a2454da52d0
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405055"
---
# <a name="windows8-whats-new-for-usb"></a>Windows 8：USB 的新增功能


本主题总结了新功能和 Windows 8 中的通用串行总线 (USB) 客户端驱动程序的改进。

-   [新的驱动程序堆栈的 USB 3.0 设备](#new-driver-stack-for-usb-30-devices)
-   [支持的新堆栈功能](#features-supported-by-the-new-stack)
-   [USB 客户端驱动程序的客户端约定版本](#client-contract-version-for-usb-client-drivers)
-   [用于分配和构建 URBs 新例程](#new-routines-for-allocating-and-building-urbs)
-   [新的用户模式 I/O 控件请求的 USB 3.0 集线器](#new-user-mode-io-control-requests-for-usb-30-hubs)
-   [新的兼容 WinUSB ID](#new-compatible-id-for-winusb)
-   [USB 客户端驱动程序的新 Visual Studio 模板 *(\*Beta 针对新功能)*](#new-visual-studio-templates-for-usb-client-drivers-new-for-beta)
-   [UASP 驱动程序](#uasp-driver)
-   [启动支持](#boot-support)
-   [增强的调试和诊断功能](#enhanced-debugging-and-diagnostic-capabilities)
-   [新的特定于 USB 的失败消息在设备管理器](#new-usb-specific-failure-messages-in-device-manager)

有关常规 USB 中新功能的信息，请参阅[USB 驱动程序的新建](https://msdn.microsoft.com/library/windows/hardware/hh451212)。

## <a name="new-driver-stack-for-usb-30-devices"></a>新的驱动程序堆栈的 USB 3.0 设备


Windows 8 提供新的 USB 驱动程序堆栈，以支持 USB 3.0 设备。 新的堆栈包括 USB 3.0 设备附加到 xHCI 主控制器时，Windows 会加载的驱动程序。 新的驱动程序基于[内核模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff557405)(KMDF)，并实现 USB 3.0 规范中定义的功能。 新的驱动程序是按如下所示：

-   Usbxhci.sys
-   Ucx01000.sys
-   Usbhub3.sys

新的驱动程序堆栈兼容的现有客户端驱动程序是在生成和早期版本的 Windows 操作系统上进行测试。

若要查看 USB 驱动程序堆栈体系结构的框图和新的驱动程序的简短说明，请参阅[USB 3.0 驱动程序堆栈体系结构](usb-3-0-driver-stack-architecture.md)。

## <a name="features-supported-by-the-new-stack"></a>支持的新堆栈功能


USB 3.0 设备的 USB 驱动程序堆栈支持许多新功能。 某些功能是由客户端驱动程序进行配置。 这些功能如下所示：

-   对于大容量终结点的静态流。

    流提供的功能来执行多个数据传输到单个批量终结点的客户端驱动程序。 Windows 8 的 Windows Driver Kit (WDK) 提供了新设备驱动程序接口 (DDIs) 允许客户端驱动程序到可以打开最多 255 流中的大容量终结点。 打开流后，客户端驱动程序可以执行数据传输到和从特定流。 有关详细信息，请参阅[如何打开和关闭 USB 大容量终结点中的静态流](how-to-open-streams-in-a-usb-endpoint.md)。

-   链接的 MDLs

    客户端驱动程序可以在一个链 MDLs 而不是连续的缓冲区中指定有效负载。 这允许要进行分段因此同时移除数量、 大小和缓冲区的对齐方式的限制的物理内存中的传输缓冲区。 使用链接的 MDLs 可以提高数据传输过程中的性能，因为它避免了双缓冲。 有关详细信息，请参阅[如何发送链接 MDL](how-to-send-chained-mdls.md)。

-   挂起函数和复合设备的远程唤醒。

    功能使复合设备进入和退出低功耗状态，独立于其他函数的函数。 功能驱动程序还可以请求由设备发起远程唤醒。 必须由复合设备的父驱动程序处理此类请求。 Microsoft 提供的父驱动程序 (Usbccgp.sys) 支持函数挂起和远程唤醒功能中。 Windows 8 的 WDK 提供了 DDIs 允许替换父驱动程序来实现这些功能。 有关详细信息，请参阅[实现函数挂起复合驱动程序中如何](how-to--implement-remote-and-function-wake-support.md)。

## <a name="client-contract-version-for-usb-client-drivers"></a>USB 客户端驱动程序的客户端约定版本


一个*客户端约定版本*标识一组客户端驱动程序时发送请求到 USB 驱动程序堆栈的规则。 如果不这样做可能会导致意外行为。 有关这些规则的信息，请参阅[最佳实践：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

计划对于 3.0 版的设备，使用 USB 驱动程序堆栈的功能的客户端驱动程序必须将自身标识与客户端协定版本为 USBD\_客户端\_协定\_版本\_602。 这样的客户端驱动程序需要注册与 USB 驱动程序堆栈。 注册后，客户端驱动程序必须查询基础的 USB 驱动程序堆栈，确定堆栈是否支持所需的功能。 为了帮助实现这些操作，以下特定于 KMDF 的方法和 WDM 例程中包含了 Windows 8 的 WDK:

| 用例                                                           | 应基于 KMDF 驱动程序...                                                                                                              | WDM 驱动程序必须...                                                                                          |
|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| 若要指定客户端协定版本和与 USB 驱动程序堆栈 | 调用[ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)方法。                                      | 调用[ **USBD\_CreateHandle** ](https://msdn.microsoft.com/library/windows/hardware/hh406241)例程。                                                |
| 若要查询特定的功能                               | 调用[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh439434)并指定查询的功能的 GUID。 | 调用[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)并指定查询的功能的 GUID。 |

 

## <a name="new-routines-for-allocating-and-building-urbs"></a>用于分配和构建 URBs 新例程


Windows 8 提供了用于分配、 格式设置，将释放 URBs 新例程。 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)结构分配的 USB 驱动程序堆栈。 如果基础堆栈是新的 USB 驱动程序堆栈，URB 配对使用不透明的 URB 上下文。 USB 驱动程序堆栈使用 URB 上下文来改进 URB 跟踪和处理。 有关例程的详细信息，请参阅[Allocating 和构建 URBs](how-to-add-xrb-support-for-client-drivers.md)。

新的例程如下所示：

-   [**USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)
-   [**USBD\_IsochUrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406231)
-   [**USBD\_SelectConfigUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406243)
-   [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://msdn.microsoft.com/library/windows/hardware/hh406245)
-   [**USBD\_UrbFree**](https://msdn.microsoft.com/library/windows/hardware/hh406252)
-   [**USBD\_AssignUrbToIoStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/hh406228)例程，以将 URB 与 IRP 相关联。 此例程仅适用于 WDM 客户端驱动程序。

除了上述列表中的例程，还有 URB 分配新的特定于 KMDF 的方法。 对于 KMDF 基于客户端驱动程序，我们建议您调用的

-   [ **WdfUsbTargetDeviceCreateUrb** ](https://msdn.microsoft.com/library/windows/hardware/hh439423)方法 (而不是[ **USBD\_UrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406250)) 来分配 URB。
-   [ **WdfUsbTargetDeviceCreateIsochUrb** ](https://msdn.microsoft.com/library/windows/hardware/hh439420)方法 (而不是[ **USBD\_IsochUrbAllocate**](https://msdn.microsoft.com/library/windows/hardware/hh406231)) 来分配 URB有关同步的传输。 这些调用分配可变的 URB 基于同步所需的传输的数据包数。 有关同步传输的详细信息，请参阅[如何将数据传输到 USB 等时终结点](transfer-data-to-isochronous-endpoints.md)。

## <a name="new-user-mode-io-control-requests-for-usb-30-hubs"></a>新的用户模式 I/O 控件请求的 USB 3.0 集线器


Windows 8 提供新 Ioctl 应用程序可以用来检索有关 USB 3.0 集线器和它们的端口的信息。 新 Ioctl 是按如下所示：

-   [**IOCTL\_USB\_获取\_中心\_信息\_EX**](https://msdn.microsoft.com/library/windows/hardware/hh450860)
-   [**IOCTL\_USB\_获取\_端口\_连接器\_属性**](https://msdn.microsoft.com/library/windows/hardware/hh450863)
-   [**IOCTL\_USB\_获取\_节点\_连接\_信息\_EX\_V2**](https://msdn.microsoft.com/library/windows/hardware/hh450861)

通过将发送到 USB 驱动程序上的 I/O 请求信息的下面一堆栈应用程序检索：

-   集线器描述符
-   所有端口和随附的端口的属性
-   连接到端口的设备的运行速度

## <a name="new-compatible-id-for-winusb"></a>新的兼容 WinUSB ID


设备制造商可以在固件 （Microsoft 操作系统功能描述符） 中添加"WINUSB"，以便该 Windows 会将设备识别为 WinUSB 设备。 在 Windows 8 中，Winusb.inf 已修改为包括 USB\\MS\_COMP\_WINUSB 作为设备标识符字符串。 所做的修改使 Windows 自动为该设备，该函数驱动程序加载 Winusb.sys，一旦检测到设备。 有关详细信息，请参阅[WinUSB 设备](automatic-installation-of-winusb.md)。

## <a name="new-visual-studio-templates-for-usb-client-drivers-new-for-beta"></a>USB 客户端驱动程序的新 Visual Studio 模板 *(\*Beta 针对新功能)*


Microsoft Visual Studio 2012 包含**USB 用户模式驱动程序**并**USB 内核模式驱动程序**分别生成 UMDF 和 KMDF USB 客户端驱动程序，起始代码的模板。 模板代码初始化要启用与硬件通信的 USB 目标设备对象。 有关详细信息，请参阅下列主题：

-   [如何编写第一个 USB 客户端驱动程序 (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)
-   [如何编写第一个 USB 客户端驱动程序 (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)

有关详细信息，请参阅[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)。 扩展您的驱动程序通过执行[USB 客户端驱动程序的常见任务](wdk-resources-for-usb-driver-development.md)。

有关如何实现 UMDF 和 KMDF 驱动程序的信息，请参阅 Microsoft Press 书籍*使用 Windows Driver Foundation 开发驱动程序*。

## <a name="uasp-driver"></a>UASP 驱动程序


Windows 8 中包含新的 USB 存储驱动程序实现 USB 附加 SCSI 协议 (UASP)。 新的驱动程序使用大容量的终结点，根据官方的 USB 3.0 规范静态流。

## <a name="boot-support"></a>启动支持


转到功能 Windows 允许 Windows 从闪存驱动器或外部驱动器启动。 您可以启动与从不同计算机上这些驱动器的 Windows 副本。

## <a name="enhanced-debugging-and-diagnostic-capabilities"></a>增强的调试和诊断功能


Windows 8 提供新的 USB 3.0 调试工具，以更快地提高诊断 USB 问题。 有新 USB 3.0 内核调试器扩展，检查 USB 3.0 主控制器和设备状态。 可以使用 USB WPP 和事件跟踪分析 USB 交互并更轻松地解决 USB 设备问题。 Windows 8 支持通过 USB 3.0 进行调试。 有关详细信息，请参阅[设置了 USB 3.0 连接手动](https://msdn.microsoft.com/library/windows/hardware/hh439372)。

## <a name="new-usb-specific-failure-messages-in-device-manager"></a>新的特定于 USB 的失败消息在设备管理器


有时，Windows 可能无法枚举已连接的 USB 设备。 通常情况下，枚举失败会发生时发送到 USB 设备的请求失败或设备返回不正确的描述符。

在 Windows 8 中，出现此类故障时，**常规**选项卡**设备管理器**显示特定于 USB 的错误消息，指明失败的原因。

错误字符串如下所示：

-   USB 设备描述符的请求失败。
-   USB 设置地址请求失败。
-   USB 端口重置请求失败。
-   不删除 USB 设备的前一个实例。
-   USB 设备返回了无效的 USB 配置描述符。
-   USB 设备返回了无效的 USB 设备描述符。
-   无法访问注册表。
-   USB 配置描述符的请求失败。
-   USB 设备的端口状态的请求失败。
-   USB 设备返回一个序列号无效字符串。
-   USB 设置 SEL 请求失败。
-   USB BOS 描述符的请求失败。
-   USB 设备限定符描述符的请求失败。
-   USB 序列号字符串描述符的请求失败。
-   USB 语言 ID 字符串描述符的请求失败。
-   USB 产品说明字符串描述符的请求失败。
-   Microsoft 操作系统的请求扩展配置描述符失败。
-   Microsoft 操作系统容器 ID 描述符的请求失败。
-   USB 设备返回了无效的 USB BOS 描述符。
-   USB 设备返回了无效的 USB 设备限定符描述符。
-   USB 设备返回了无效的 USB 语言 ID 字符串描述符。
-   USB 设备返回了无效的 Microsoft 操作系统容器 ID 描述符。
-   USB 设备返回无效的 Microsoft 操作系统扩展配置描述符。
-   USB 设备返回了无效的产品说明字符串描述符。
-   USB 设备返回的序列号无效字符串描述符。

## <a name="related-topics"></a>相关主题
[USB 驱动程序的新增功能](https://msdn.microsoft.com/library/windows/hardware/hh451212)  
[通用串行总线 (USB) 驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



