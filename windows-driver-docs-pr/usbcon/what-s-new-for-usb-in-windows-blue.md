---
Description: 下面是 Windows 8.1 中通用串行总线（USB）的新功能和改进。
title: Windows 8.1-USB 的新增功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce6171bcef7118b24ba3a43fea7b520b4b369c6c
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210143"
---
# <a name="windows-81-whats-new-for-usb"></a>Windows 8.1： USB 的新增功能


下面是 Windows 8.1 中通用串行总线（USB）的新功能和改进。

-   [用于开发 UWP 应用的 Windows 运行时 USB API](#windows-runtime-usb-api-for-developing-uwp-apps)
-   [用于改进设备枚举的 Microsoft 操作系统2.0 描述符](#microsoft-os-20-descriptors-for-improved-device-enumerations)
-   [对 WinUSB 的同步支持](#isochronous-support-for-winusb)
-   [USB 驱动程序堆栈改进](#usb-driver-stack-improvements)
-   [硬件认证包（HCK）中的 USB 测试](#usb-tests-in-the-hardware-certification-kit-hck)
-   [改进的 USB 诊断工具和调试器扩展](#improved-usb-diagnostic-tools-and-debugger-extensions)
-   [相关主题](#related-topics)

## <a name="windows-runtime-usb-api-for-developing-uwp-apps"></a>用于开发 UWP 应用的 Windows 运行时 USB API


Windows 运行时提供了一个新的命名[**空间：/VB/**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb) （请参阅[编写适用于 Usb 设备的应用（使用C#C++的 UWP 应用）](https://docs.microsoft.com/previous-versions/windows/apps/dn263144(v=win.10))以获取简短概述）。 通过使用命名空间，可以编写与自定义 USB 设备通信的 UWP 应用。

有关详细信息，请参阅以下主题：

-   [与 USB 设备通信，开始完成（UWP 应用）](talking-to-usb-devices-start-to-finish.md)
-   [如何将 USB 设备功能添加到应用程序清单](updating-the-app-manifest-with-usb-device-capabilities.md)
-   [如何连接到 USB 设备（UWP 应用）](how-to-connect-to-a-usb-device--uwp-app-.md)
-   [如何发送 USB 控件传输（UWP 应用）](how-to-send-a-usb-control-transfer--uwp-app-.md)
-   [如何发送 USB 中断传输请求（UWP 应用）](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)
-   [如何发送 USB 批量传输请求（UWP 应用）](how-to-send-a-usb-bulk-transfer--uwp-app-.md)
-   [如何获取 USB 描述符（UWP 应用）](how-to-get-usb-descriptors--uwp-app-.md)
-   [如何选择 USB 接口设置（UWP 应用）](how-to-select-a-usb-interface-setting--uwp-app-.md)

这些示例演示如何使用[**Windows. Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)命名空间。

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
<td><p><a href="" id="custom-usb-device-access-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">自定义 USB 设备访问示例</a></p></td>
<td><p>此示例演示如何与 USB 设备通信。 该示例可以与 OSR USB FX2 学习工具包和 SuperMUTT 设备通信。</p></td>
</tr>
<tr class="even">
<td><p><a href="" id="usb-cdc-control-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC 控制示例</a></p></td>
<td><p>此示例演示如何与 USB CDC （通信设备类）设备进行通信，以及如何通过串行端口（例如 USB 串行转换器电缆）发送和接收数据。</p></td>
</tr>
<tr class="odd">
<td><p><a href="" id="firmware-update-usb-device-sample"></a><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">固件更新 USB 设备示例</a></p></td>
<td><p>此示例演示 UWP 应用如何可以更新 USB 设备的固件。 更新操作作为后台任务运行。</p></td>
</tr>
</tbody>
</table>

## <a name="microsoft-os-20-descriptors-for-improved-device-enumerations"></a>用于改进设备枚举的 Microsoft 操作系统2.0 描述符 
 
Microsoft 操作系统2.0 描述符改善了设备标识和驱动程序安装体验。

MS OS 2.0 描述符规范提供以下改进：

-   定义一个新的 BOS 设备功能描述符，以允许设备返回特定于平台的属性。 BOS 描述符是由标准 USB 规范为 USB 版本2.1 和更高版本定义的标准描述符，因此检索是正常的和预期的枚举步骤，不应导致意外的设备行为。
-   允许描述符的作用域为整个设备、特定配置或函数。
-   允许设备返回多个描述符集，其中每个集都适用于特定范围的 Windows 版本。 这允许设备根据其附加到的系统上的 Windows 版本进行不同的枚举。
-   更快恢复：设备可以识别其恢复时间，从而减少挂起状态的时间。

有关规范的信息，请参阅[适用于 USB 设备的 MICROSOFT OS 描述符](microsoft-defined-usb-descriptors.md)。

## <a name="isochronous-support-for-winusb"></a>对 WinUSB 的同步支持


Microsoft 提供的 WinUSB （内核模式驱动程序）现在支持与 USB 设备的同步终结点进行传输

用户模式 DLL Winusb 公开这些[Winusb 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)，Windows 桌面应用程序可使用这些函数启动此类传输。

-   [**WinUsb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)
-   [**WinUsb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)
-   [**WinUsb\_WriteIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)
-   [**WinUsb\_ReadIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)
-   [**WinUsb\_WriteIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)
-   [**WinUsb\_ReadIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)
-   [**WinUsb\_GetCurrentFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber)
-   [**WinUsb\_GetAdjustedFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber)

## <a name="usb-driver-stack-improvements"></a>USB 驱动程序堆栈改进


在 Windows 8.1 中，USB 3.0 和2.0 驱动程序堆栈的性能和可靠性都得到了改进。

-   对于支持 InstantGo 的更新平台，S0 中整体的系统功率消耗可能极低。 对于此类系统，即使是 USB 设备在选择性挂起期间消耗的几个毫瓦，也会非常重要。 由于优化了新系统的强大功能，我们实现了 D3cold 的 USB 2.0 堆栈和 Usbccgp，并改进了 USB 3.0 驱动程序堆栈的 Windows 8 实现。
-   在未安装驱动程序时提供更好的电源管理。 如果连接到控制器的设备是唯一的，则 USB 驱动程序堆栈会挂起导致集线器挂起的 USB 端口。
-   已改进 DPC 性能以避免监视程序超时。
-   设备现在可以恢复速度快于 USB 2.0 规范中指定的默认10毫秒。 另外，主机控制器驱动程序断言会继续发出信号，在这种情况下，USB 2.0 规范中所需的时间少于20毫秒。
-   在执行控制、大容量和同步数据传输时，USB 3.0 驱动程序堆栈现在更可靠。

## <a name="usb-tests-in-the-hardware-certification-kit-hck"></a>硬件认证包（HCK）中的 USB 测试

-   硬件认证包（HCK）中的这些 USB 测试已改进。 设备枚举测试现在包含一个新的参数，可在使用简化拓扑进行测试的过程中减少手动干预。 挂起测试已改进日志记录功能。

    -   [USB 公开端口控制器测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh998021(v=vs.85))
    -   [USB 集线器公开端口测试 USB](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj123960(v=vs.85))
    -   [集线器选择性挂起测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124844(v=vs.85))
    -   [USB 公开的端口系统测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj123655(v=vs.85))
    -   [USB 选择性挂起测试（xHCI）](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124491(v=vs.85))
    -   [USB 3.0 挂起测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj125210(v=vs.85))
-   MUTT 和 SuperMUTT 设备现在为 USB-IF 合规性设备。 设备和随附的软件包会集成到 HCK 套件的 USB 测试。 它们提供的自动化测试可以在 USB 控制器、设备和系统的开发周期中使用，尤其是在进行压力测试时使用。

    可以从[JJG 技术](https://jjgtechnologies.com/mutt.md)购买 MUTT 硬件。 设备未安装安装的固件。 若要安装固件，请从[该网站](https://msdn.microsoft.com/windows/hardware/jj590752)下载 MUTT 软件包并运行 MUTTUtil。 有关详细信息，请参阅包附带的文档。

## <a name="improved-usb-diagnostic-tools-and-debugger-extensions"></a>改进的 USB 诊断工具和调试器扩展


-   USB 2.0 和3.0 （USBKD 和 USB3KD）的内核调试扩展已改进为具有类似的命令模式。 Usbccgp 的调试器扩展现已可用。
-   消息分析器（Netmon）中显示的 USB 事件现在更具描述性。 事件也可以按控制器、中心等进行分组和排序。

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



