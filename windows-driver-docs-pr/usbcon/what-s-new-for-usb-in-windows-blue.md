---
Description: 以下是新功能和改进的通用串行总线 (USB) 在 Windows 8.1。
title: Windows 8.1-什么是 USB 的新增功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e7c846902fe660db70227bde70c3a06577e803d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389191"
---
# <a name="windows-81-whats-new-for-usb"></a>Windows 8.1：USB 的新增功能


以下是新功能和改进的通用串行总线 (USB) 在 Windows 8.1。

-   [有关开发 UWP 应用的 Windows 运行时 USB API](#usb-sdk)
-   [Microsoft OS 2.0 描述符的改进了的设备枚举](#microsoft-os-2-0-descriptors-for-improved-device-enumeration)
-   [对 WinUSB 等时支持](#usb-wdk)
-   [USB 驱动程序堆栈改进](#usb-driver-stack-improvements)
-   [USB 测试硬件认证包 (HCK) 中](#usb-tests-in-the-hardware-certification-kit-hck)
-   [改进了的 USB 的诊断工具和调试器扩展](#improved-usb-diagnostic-tools-and-debugger-extensions-)
-   [相关的主题](#related-topics)

## <a name="windows-runtime-usb-api-for-developing-uwp-apps"></a>有关开发 UWP 应用的 Windows 运行时 USB API


Windows 运行时提供新的命名空间：[**Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466) (请参阅[编写的 USB 设备的应用 (UWP 应用使用C#/VB/C++)](https://msdn.microsoft.com/library/windows/apps/xaml/dn263144)的简要概述)。 通过使用命名空间，可以编写与自定义的 USB 设备进行通信的 UWP 应用。

有关详细信息，请参阅以下主题：

-   [与 USB 设备通信，启动以完成 （UWP 应用）](talking-to-usb-devices-start-to-finish.md)
-   [如何将 USB 设备功能添加到应用程序清单](updating-the-app-manifest-with-usb-device-capabilities.md)
-   [如何连接到 USB 设备 （UWP 应用）](how-to-connect-to-a-usb-device--uwp-app-.md)
-   [如何发送 USB 控制传输 （UWP 应用）](how-to-send-a-usb-control-transfer--uwp-app-.md)
-   [如何发送 USB 中断传输请求 （UWP 应用）](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)
-   [如何将发送的 USB 大容量传输请求 （UWP 应用）](how-to-send-a-usb-bulk-transfer--uwp-app-.md)
-   [如何获取 USB 描述符 （UWP 应用）](how-to-get-usb-descriptors--uwp-app-.md)
-   [如何选择 USB 接口设置 （UWP 应用）](how-to-select-a-usb-interface-setting--uwp-app-.md)

这些示例演示了如何使用[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)命名空间。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>UWP 应用示例</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="" id="custom-usb-device-access-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">自定义的 USB 设备访问示例</a></p></td>
<td><p>此示例演示如何与 USB 设备进行通信。 该示例可以与 OSR USB FX2 学习工具包和 SuperMUTT 设备通信。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="usb-cdc-control-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC 控制示例</a></p></td>
<td><p>此示例演示如何与 USB CDC （通信设备类） 设备通信以及发送和接收数据通过串行端口，例如 USB 串行转换器电缆。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="firmware-update-usb-device-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">固件更新 USB 设备示例</a></p></td>
<td><p>此示例演示如何为 UWP 应用可以更新 USB 设备的固件。 更新操作作为后台任务运行。</p></td>
</tr>
</tbody>
</table>

## <a name="microsoft-os-20-descriptors-for-improved-device-enumerations"></a>改进了的设备枚举 Microsoft OS 2.0 描述符 
 
Microsoft OS 2.0 描述符提高设备标识和驱动程序安装体验。

MS OS 2.0 描述符规范提供了以下改进：

-   定义新的 BOS 设备功能描述符允许设备返回特定于平台的属性。 BOS 描述符是标准描述符规范所定义的标准 USB USB 版本 2.1 和更高版本，因此检索常规和应不会导致意外的设备行为的预期的枚举步骤。
-   允许描述符来为作用域为整个设备、 特定配置或函数。
-   允许设备返回多个描述符集，其中每个集适用于特定的 Windows 版本。 这使得设备枚举以不同的方式根据附加到系统上的 Windows 版本。
-   更快地恢复：设备可以识别其恢复时间，从而减少了时间从挂起状态。

有关规范的信息，请参阅[USB 设备的 Microsoft 操作系统描述符](microsoft-defined-usb-descriptors.md)。

## <a name="isochronous-support-for-winusb"></a>对 WinUSB 等时支持


Microsoft 提供 WinUSB （内核模式驱动程序） 现在支持在 USB 设备的同步终结点的传输

用户模式 DLL，Winusb.dll，公开这些[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)Windows 桌面应用程序可用于启动此类传输。

-   [**WinUsb\_RegisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265566)
-   [**WinUsb\_UnregisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265567)
-   [**WinUsb\_WriteIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265569)
-   [**WinUsb\_ReadIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265565)
-   [**WinUsb\_WriteIsochPipe**](https://msdn.microsoft.com/library/windows/hardware/dn265568)
-   [**WinUsb\_ReadIsochPipe**](https://msdn.microsoft.com/library/windows/hardware/dn265564)
-   [**WinUsb\_GetCurrentFrameNumber**](https://msdn.microsoft.com/library/windows/hardware/dn265549)
-   [**WinUsb\_GetAdjustedFrameNumber**](https://msdn.microsoft.com/library/windows/hardware/dn265548)

## <a name="usb-driver-stack-improvements"></a>USB 驱动程序堆栈改进


在 Windows 8.1 中的性能和可靠性的 USB 3.0 和 2.0 的驱动程序堆栈进行了改进。

-   对于更高版本支持 InstantGo 的平台，S0 中的整体系统电源消耗可能是极低。 对于此类系统，甚至几个为毫瓦的 USB 设备使用的在中选择性挂起，请开始很重要。 目标是优化的电源可用于新系统，我们实现了 D3cold USB 2.0 堆栈和 Usbccgp.sys 和 USB 3.0 驱动程序堆栈的改进了的 Windows 8 实现。
-   不安装任何驱动程序时，更好地电源管理。 USB 驱动程序堆栈现在挂起会使中心将挂起如果它是唯一的设备连接到控制器的 USB 端口。
-   DPC 性能进行了改进，以避免监视器超时崩溃。
-   设备现在可以比默认值为 10 毫秒 USB 2.0 规范中指定的时间更快地恢复。 此外，主机控制器驱动程序断言恢复小于 20 毫秒在 USB 2.0 规范所需的信号。
-   执行控制、 批量和同步数据传输时，USB 3.0 驱动程序堆栈现更可靠。

## <a name="usb-tests-in-the-hardware-certification-kit-hck"></a>USB 测试硬件认证包 (HCK) 中

-   改进了这些 USB 测试硬件认证包 (HCK) 中。 设备枚举测试现可使用简化的拓扑进行测试期间的降低手动干预的新参数。 挂起测试已改进的日志记录功能。

    -   [USB 公开的端口控制器测试](https://msdn.microsoft.com/library/windows/hardware/hh998021.aspx)
    -   [USB 集线器公开端口测试 USB](https://msdn.microsoft.com/library/windows/hardware/jj123960.aspx)
    -   [中心选择性挂起测试](https://msdn.microsoft.com/library/windows/hardware/jj124844.aspx)
    -   [USB 公开的端口系统测试](https://msdn.microsoft.com/library/windows/hardware/jj123655.aspx)
    -   [USB 选择性挂起测试 (xHCI)](https://msdn.microsoft.com/library/windows/hardware/jj124491.aspx)
    -   [USB 3.0 挂起测试](https://msdn.microsoft.com/library/windows/hardware/jj125210.aspx)
-   MUTT 和 SuperMUTT 设备现 USB-如果符合要求的设备。 设备和随附的软件程序包中集成到 HCK 的 USB 测试套件。 它们提供的自动化测试可以在 USB 控制器、设备和系统的开发周期中使用，尤其是在进行压力测试时使用。

    可以从购买 MUTT 硬件[JJG 技术](http://jjgtechnologies.com/mutt.md)。 设备没有安装的已安装的固件。 若要安装固件，下载从 MUTT 软件包[此网站](https://msdn.microsoft.com/windows/hardware/jj590752)并运行 MUTTUtil.exe。 有关详细信息，请参阅随程序包提供的文档。

## <a name="improved-usb-diagnostic-tools-and-debugger-extensions"></a>改进了的 USB 的诊断工具和调试器扩展


-   USB 2.0 和 3.0 （USBKD.dll 和 USB3KD.dll） 的内核调试扩展已经过改进，具有类似的命令模式。 Usbccgp.sys 的调试器扩展现已推出。
-   在 Message Analyzer (Netmon) 中所示的 USB 事件现已更具描述性。 这些事件还可进行分组和按控制器、 中心和等等。

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



