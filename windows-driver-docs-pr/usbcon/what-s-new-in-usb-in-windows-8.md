---
description: 本主题概述了 Windows 8 中的通用串行总线 (USB) 客户端驱动程序的新增功能和改进。
title: Windows 8-USB 的新增功能
ms.date: 05/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6d95ed4ff69f20ee1297864456ecbed16ab33f39
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969060"
---
# <a name="windows8-whats-new-for-usb"></a>Windows 8：USB 的新增功能


本主题概述了 Windows 8 中的通用串行总线 (USB) 客户端驱动程序的新增功能和改进。

-   [用于 USB 3.0 设备的新驱动程序堆栈](#new-driver-stack-for-usb-30-devices)
-   [新堆栈支持的功能](#features-supported-by-the-new-stack)
-   [USB 客户端驱动程序的客户端协定版本](#client-contract-version-for-usb-client-drivers)
-   [用于分配和生成 URBs 的新例程](#new-routines-for-allocating-and-building-urbs)
-   [USB 3.0 集线器的新用户模式 i/o 控制请求](#new-user-mode-io-control-requests-for-usb-30-hubs)
-   [WinUSB 的新的兼容 ID](#new-compatible-id-for-winusb)
-   [适用于 USB 客户端驱动程序的新 Visual Studio 模板 * (\* 适用于 Beta) 的新 *](#new-visual-studio-templates-for-usb-client-drivers-new-for-beta)
-   [UASP 驱动程序](#uasp-driver)
-   [启动支持](#boot-support)
-   [增强的调试和诊断功能](#enhanced-debugging-and-diagnostic-capabilities)
-   [设备管理器中的新的 USB 特定失败消息](#new-usb-specific-failure-messages-in-device-manager)

有关 USB 中的新增功能的一般信息，请参阅 [Usb 驱动程序的新增](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development)功能。

## <a name="new-driver-stack-for-usb-30-devices"></a>用于 USB 3.0 设备的新驱动程序堆栈


Windows 8 提供了一个新的 USB 驱动程序堆栈以支持 USB 3.0 设备。 新堆栈包含 Windows 在将 USB 3.0 设备连接到 xHCI 主机控制器时加载的驱动程序。 新驱动程序基于 [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development) (KMDF) 并实现 USB 3.0 规范中定义的功能。 新驱动程序如下所示：

-   Usbxhci.sys
-   Ucx01000.sys
-   Usbhub3.sys

新的驱动程序堆栈保持与早期版本的 Windows 操作系统上生成和测试的现有客户端驱动程序的兼容性。

若要查看 USB 驱动程序堆栈的体系结构框图和新驱动程序的简要说明，请参阅 [usb 3.0 驱动程序堆栈体系结构](usb-3-0-driver-stack-architecture.md)。

## <a name="features-supported-by-the-new-stack"></a>新堆栈支持的功能


USB 3.0 设备的 USB 驱动程序堆栈支持许多新功能。 某些功能是由客户端驱动程序配置的。 这些功能如下所示：

-   大容量终结点的静态流。

    流提供了客户端驱动程序，能够对单个大容量终结点执行多个数据传输。 Windows 8 的 Windows 驱动程序工具包 (WDK) 提供 (DDIs) 的新设备驱动程序接口，该接口允许客户端驱动程序在大容量终结点中打开最多255流。 打开流后，客户端驱动程序可以执行与特定流之间的数据传输。 有关详细信息，请参阅 [如何在 USB 大容量终结点中打开和关闭静态流](how-to-open-streams-in-a-usb-endpoint.md)。

-   链式 MDLs

    客户端驱动程序可以在 MDLs （而不是连续的）链中指定负载。 这允许在物理内存中分段传输缓冲区，从而删除缓冲区的数量、大小和对齐方式的限制。 使用链式 MDLs 可以提高数据传输过程中的性能，因为这样可以避免双重缓冲。 有关详细信息，请参阅 [如何发送链式 MDL](how-to-send-chained-mdls.md)。

-   复合设备的 "挂起" 和 "远程唤醒" 功能。

    此功能使复合设备的功能能够进入和退出低功耗状态，而与其他功能无关。 函数驱动程序还可以请求设备启动的远程唤醒。 此类请求必须由复合设备的父驱动程序处理。 Microsoft 提供的父驱动程序 ( # A0) 支持函数挂起和远程唤醒功能。 适用于 Windows 8 的 WDK 提供 DDIs，允许替换父驱动程序实现这些功能。 有关详细信息，请参阅 [如何在复合驱动程序中实现函数挂起](how-to--implement-remote-and-function-wake-support.md)。

## <a name="client-contract-version-for-usb-client-drivers"></a>USB 客户端驱动程序的客户端协定版本


*客户端合同版本*标识客户端驱动程序向 USB 驱动程序堆栈发送请求时的一组规则。 否则，可能会导致意外的行为。 有关这些规则的信息，请参阅 [最佳做法：使用 URBs](usb-client-driver-contract-in-windows-8.md)。

要使用适用于3.0 设备的 USB 驱动程序堆栈功能的客户端驱动程序，必须使用 USBD \_ 客户端 \_ 合同 \_ 版本602的客户端合同版本来标识自身 \_ 。 需要使用此类客户端驱动程序才能向 USB 驱动程序堆栈进行注册。 注册之后，客户端驱动程序必须查询基础 USB 驱动程序堆栈，以确定堆栈是否支持所需的功能。 为了便于执行这些操作，在 Windows 8 的 WDK 中包括了以下 KMDF 特定的方法和 WDM 例程：

| 用例                                                           | 基于 KMDF 的驱动程序应 .。。                                                                                                              | WDM 驱动程序必须 .。。                                                                                          |
|--------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| 指定客户端协定版本和 USB 驱动程序堆栈 | 调用 [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) 方法。                                      | 调用 [**USBD \_ CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle) 例程。                                                |
| 查询特定功能                               | 调用 [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability) 并指定要查询的功能的 GUID。 | 调用 [**USBD \_ QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)) 并指定要查询的功能的 GUID。 |

 

## <a name="new-routines-for-allocating-and-building-urbs"></a>用于分配和生成 URBs 的新例程


Windows 8 提供了用于分配、格式化和释放 URBs 的新例程。 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)结构由 USB 驱动程序堆栈分配。 如果基础堆栈是新的 USB 驱动程序堆栈，则 URB 与不透明的 URB 上下文配对。 USB 驱动程序堆栈使用 URB 上下文来改善 URB 跟踪和处理。 有关例程的详细信息，请参阅 [分配和生成 URBs](how-to-add-xrb-support-for-client-drivers.md)。

新例程如下所示：

-   [**USBD \_ UrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)
-   [**USBD \_ IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)
-   [**USBD \_ SelectConfigUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)
-   [**USBD \_ SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)
-   [**USBD \_ UrbFree**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urbfree)
-   [**USBD \_AssignUrbToIoStackLocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_assignurbtoiostacklocation) 例程将 URB 与 IRP 关联。 此例程仅适用于 WDM 客户端驱动程序。

除了前面的列表中的例程外，还提供了用于 URB 分配的新的、特定于 KMDF 的方法。 对于基于 KMDF 的客户端驱动程序，我们建议你调用，

-   [**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)方法 (而不是[**USBD \_ URBALLOCATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)) 来分配 URB。
-   [**WdfUsbTargetDeviceCreateIsochUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)方法 (而不是[**USBD \_ IsochUrbAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_isochurballocate)) 为同步传输分配 URB。 这些调用会根据传输所需的同步数据包数分配一个大小可变的 URB。 有关同步传输的详细信息，请参阅 [如何将数据传输到 USB 同步终结点](transfer-data-to-isochronous-endpoints.md)。

## <a name="new-user-mode-io-control-requests-for-usb-30-hubs"></a>USB 3.0 集线器的新用户模式 i/o 控制请求


Windows 8 提供了新的 IOCTLs，应用程序可以使用它们来检索有关 USB 3.0 集线器及其端口的信息。 新 IOCTLs 如下所示：

-   [**IOCTL \_ USB \_ 获取 \_ 集线器 \_ 信息， \_ 例如**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_hub_information_ex)
-   [**IOCTL \_ USB \_ 获取 \_ 端口 \_ 连接器 \_ 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_port_connector_properties)
-   [**IOCTL \_ USB \_ 获取 \_ 节点 \_ 连接 \_ 信息， \_ 例如 \_ V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_node_connection_information_ex_v2)

通过向 USB 驱动程序堆栈发送前面的 i/o 请求，应用程序将检索以下信息集：

-   中心描述符
-   所有端口和辅助端口的属性
-   挂接到端口的设备的运行速度

## <a name="new-compatible-id-for-winusb"></a>WinUSB 的新的兼容 ID


设备制造商可以在 (Microsoft OS 功能描述符) 的固件中添加 "WINUSB"，以便 Windows 将设备识别为 WinUSB 设备。 在 Windows 8 中，已将 Winusb 修改为包含 USB \\ MS \_ COMP \_ Winusb 作为设备标识符字符串。 这样一来，一旦检测到设备，Windows 便会自动将 Winusb.sys 加载为设备的函数驱动程序。 有关详细信息，请参阅 [WinUSB 设备](automatic-installation-of-winusb.md)。

## <a name="new-visual-studio-templates-for-usb-client-drivers-new-for-beta"></a>适用于 USB 客户端驱动程序的新 Visual Studio 模板 * (\* 适用于 Beta) 的新 *


Microsoft Visual Studio 2012 包括 **Usb 用户模式驱动程序** 和 **Usb 内核模式驱动程序** 模板，分别为 UMDF 和 KMDF USB 客户端驱动程序生成起始代码。 模板代码初始化 USB 目标设备对象，以启用与硬件的通信。 有关详细信息，请参阅下列主题：

-   [如何编写第一个 USB 客户端驱动程序 (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)
-   [如何编写第一个 USB 客户端驱动程序 (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)

有关详细信息，请参阅 [USB 客户端驱动程序开发](getting-started-with-usb-client-driver-development.md)入门。 通过执行 [USB 客户端驱动程序的常见任务](wdk-resources-for-usb-driver-development.md)来扩展驱动程序。

有关如何实现 UMDF 和 KMDF 驱动程序的信息，请参阅 Microsoft 新闻簿 *通过 Windows Driver Foundation 开发驱动程序*。

## <a name="uasp-driver"></a>UASP 驱动程序


Windows 8 包含一个新的 USB 存储驱动程序，该驱动程序实现 USB 连接的 SCSI 协议 (UASP) 。 新驱动程序将静态流用于大容量终结点，就像使用官方的 USB 3.0 规范一样。

## <a name="boot-support"></a>启动支持


Windows to 中转功能允许 Windows 从闪存驱动器或外部驱动器启动。 你可以从不同计算机上的这些驱动器中的 Windows 副本启动。

## <a name="enhanced-debugging-and-diagnostic-capabilities"></a>增强的调试和诊断功能


Windows 8 提供了新的 USB 3.0 调试工具，提高诊断 USB 问题的速度。 有新的 USB 3.0 内核调试器扩展，可检查 USB 3.0 主机控制器和设备状态。 可以使用 USB WPP 和事件跟踪来分析 USB 交互，并更轻松地排查 USB 设备问题。 Windows 8 支持通过 USB 3.0 进行调试。 有关详细信息，请参阅 [手动设置 USB 3.0 连接](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-usb-3-0-debug-cable-connection)。

## <a name="new-usb-specific-failure-messages-in-device-manager"></a>设备管理器中的新的 USB 特定失败消息


有时，Windows 可能无法枚举连接的 USB 设备。 通常，当发送到 USB 设备的请求失败或设备返回错误的描述符时，会发生枚举失败。

在 Windows 8 中，当发生此类故障时，**设备管理器**中的 "**常规**" 选项卡将显示特定于 USB 的错误消息，指出失败的原因。

错误字符串如下：

-   对 USB 设备描述符的请求失败。
-   USB 设置地址请求失败。
-   USB 端口重置请求失败。
-   未删除 USB 设备的上一个实例。
-   USB 设备返回了无效的 USB 配置描述符。
-   USB 设备返回的 USB 设备描述符无效。
-   无法访问注册表。
-   对 USB 配置描述符的请求失败。
-   USB 设备端口状态的请求失败。
-   USB 设备返回的序列号字符串无效。
-   USB 设置 SEL 请求失败。
-   对 USB BOS 描述符的请求失败。
-   USB 设备限定符描述符的请求失败。
-   请求 USB 序列号字符串描述符失败。
-   对 USB 语言 ID 字符串描述符的请求失败。
-   对 USB 产品描述字符串描述符的请求失败。
-   Microsoft 操作系统扩展配置描述符的请求失败。
-   Microsoft OS 容器 ID 描述符的请求失败。
-   USB 设备返回了无效的 USB BOS 描述符。
-   USB 设备返回的 USB 设备限定符描述符无效。
-   USB 设备返回的 USB 语言 ID 字符串描述符无效。
-   USB 设备返回的 Microsoft OS 容器 ID 描述符无效。
-   USB 设备返回了无效的 Microsoft 操作系统扩展配置描述符。
-   USB 设备返回的产品描述字符串描述符无效。
-   USB 设备返回的序列号字符串描述符无效。

## <a name="related-topics"></a>相关主题
[USB 驱动程序的新](https://docs.microsoft.com/windows-hardware/drivers/what-s-new-in-driver-development)  
[ (USB) 驱动程序的通用串行总线](https://docs.microsoft.com/windows-hardware/drivers/)  



