---
Description: This topic describes the USB hardware verifier tool (USB3HWVerifierAnalyzer.exe) that is used for testing and debugging specific hardware events.
title: USB 硬件验证程序 (USB3HWVerifierAnalyzer.exe)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8b410e79dc93cdd79d55a89e97169ae127acd78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577041"
---
# <a name="usb-hardware-verifier-usb3hwverifieranalyzerexe"></a>USB 硬件验证程序 (USB3HWVerifierAnalyzer.exe)


本主题介绍用于测试和调试特定硬件事件的 USB 硬件验证程序工具 (USB3HWVerifierAnalyzer.exe)。

大多数硬件问题的表现在会导致不佳的最终用户体验的方面，并通常很难确定确切的失败。 捕获的设备、 端口、 集线器、 控制器或它们之间的组合中发生硬件故障，旨在 USB 硬件验证工具。

USB 硬件验证工具可以执行这些任务：

-   捕获硬件事件，并实时显示的信息。
-   生成包含所有事件的相关信息的跟踪文件。
-   分析事件信息的现有跟踪文件。

本主题包含以下各节：

-   [获取分析器工具的 USB 硬件验证工具](#getting-the-usb-hardware-verifier-analyzer-tool)
-   [如何通过使用 USB 硬件验证工具捕获的事件](#how-to-capture-events-by-using-a-usb-hardware-verifier)
-   [USB 硬件验证程序标志](#usb-hardware-verifier-flags)

## <a name="getting-the-usb-hardware-verifier-analyzer-tool"></a>获取分析器工具的 USB 硬件验证工具


USB 硬件验证工具是附带可用于下载 MUTT 软件包[MUTT 软件包中的工具](mutt-software-package.md)。

此工具包包含执行压力和传输测试 （包括 power 转换） 和 SuperSpeed 测试的几个工具。 包还具有 （可作为单独的下载） 的自述文件文档。 文档提供的 MUTT 硬件类型的简要概述。 它提供了分步指导，了解各种测试应运行，并建议的控制器、 中心、 设备、 拓扑和 BIOS/UEFI 测试。

## <a name="how-to-capture-events-by-using-a-usb-hardware-verifier"></a>如何通过使用 USB 硬件验证工具捕获的事件


若要通过使用硬件验证工具捕获事件，请执行以下步骤：

1. 通过在提升的命令提示符运行此命令启动一个会话。

   ``` syntax
   USB3HWVerifierAnalyzer.exe
   ```

   该工具支持以下选项：

   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th>选项</th>
   <th>描述</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td><p><a href="" id="---v--vendorid-"></a> -v &lt;VendorID&gt;</p></td>
   <td><p>记录指定 VendorID 硬件验证工具的所有事件。</p></td>
   </tr>
   <tr class="even">
   <td><p><a href="" id="----p--productid-"></a> -p &lt;ProductID&gt;</p></td>
   <td><p>记录指定的 ProductID 硬件验证工具的所有事件。</p></td>
   </tr>
   <tr class="odd">
   <td><p><a href="" id="-f--etl-file-"></a>-f &lt;ETL 文件&gt;</p></td>
   <td><p>分析指定的 ETL 文件。 不支持实时分析。 使用此选项，该工具将分析文件脱机。</p></td>
   </tr>
   <tr class="even">
   <td><p>/v 输出</p></td>
   <td><p>向控制台显示所有事件。</p></td>
   </tr>
   </tbody>
   </table>

     

2. 运行测试方案中你想要捕获硬件的事件。

   会话期间，USB 硬件验证工具捕获硬件事件有关的信息，在发生。 如果你想要筛选特定硬件的事件，指定 VendorId 和硬件的 ProductId。 该工具可能不会捕获一些信息 （如 VID/PID) 有关的事件的设备获取完全枚举之前发生。 缺少的信息现已推出 （接下来将讨论） 的会话结束时生成详细报告。

   下面是硬件验证工具的示例输出：

   ``` syntax
   Session Name : TraceSessionWedJun062021182012

   Attempting to start session TraceSessionWedJun062021182012...
   Trace Session created...Status : 0

   Provider Enable Success, Status : 0

   Provider Enable Success, Status : 0

   Provider Enable Success, Status : 0

   Provider Enable Success, Status : 0

   Provider Enable Success, Status : 0
   12983512883.067484s: (UsbHub3/176):
           Event Message:DescriptorValidationError20HubPortPwrCtrlMaskZero
           VendorID/ProductID: 0x451/0x2077
           DeviceInterfacePath: \??\USB#VID_0451&PID_2077#6&c4be011&0&2#{f18a0e88-c30c-11d0-8815-00a0c906bed8}
           DeviceDescription: Generic USB Hub
           PortPath:  0x2, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512888.452400s: (UsbHub3/173)
           Event Message: SuperSpeed Device is Connected on the 2.0 Bus:
           PortPath:  0x2, 0x4, 0x0, 0x0, 0x0, 0x0
   12983512900.098652s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098654s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098656s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098658s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098658s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.098660s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.099415s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorStringMismatchBetweenBlengthAndBufferLength
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
   12983512900.100168s: (UsbHub3/176):
           Event Message:DescriptorValidationErrorStringMismatchBetweenBlengthAndBufferLength
           PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0

   Provider disable Success, Status : 0

   Provider disable Success, Status : 0

   Provider disable Success, Status : 0

   Provider disable Success, Status : 0

   Provider disable Success, Status : 0

   Session Stopped...Status : 0
   ```

3. 通过按 CTRL + C 停止会话。

   在会话结束时，在当前目录中添加一个名为 AllEvents.etl 文件。 此文件包含有关在会话期间捕获的所有事件的跟踪信息。

   除了 AllEvents.etl，命令窗口中显示的报表。 该报告实时输出中包括错过了某些信息。 下面的输出显示前面的会话的示例测试报告。 此报表显示 USB 硬件验证工具遇到的所有事件。

   ``` syntax
   Record #1 (Key = 0x57ff0de4858)
     VendorID/ProductID: 0x451/0x2077
     DeviceInterfacePath: \??\USB#VID_0451&PID_2077#6&c4be011&0&2#{f18a0e88-c30c-11d0-8815-00a0c906bed8}
     DeviceDescription: Generic USB Hub
     PortPath:  0x2, 0x0, 0x0, 0x0, 0x0, 0x0
     All errors encountered:
   #1: (UsbHub3/176): DescriptorValidationError20HubPortPwrCtrlMaskZero
   #2: (UsbHub3/179): Client Initiated Recovery Action
   #3: (UsbHub3/179): Client Initiated Recovery Action
   #4: (UsbHub3/179): Client Initiated Recovery Action
   #5: (UsbHub3/179): Client Initiated Recovery Action
   #6: (UsbHub3/179): Client Initiated Recovery Action
   #7: (UsbHub3/179): Client Initiated Recovery Action
   #8: (UsbHub3/179): Client Initiated Recovery Action
   #9: (UsbHub3/179): Client Initiated Recovery Action
   #10: (UsbHub3/179): Client Initiated Recovery Action
   #11: (UsbHub3/179): Client Initiated Recovery Action
   #12: (UsbHub3/179): Client Initiated Recovery Action
   #13: (UsbHub3/179): Client Initiated Recovery Action
   #14: (UsbHub3/179): Client Initiated Recovery Action

   Record #2 (Key = 0x57ff62a36a8)
     VendorID/ProductID: 0x1058/0x740
     DeviceInterfacePath: \??\USB#VID_1058&PID_0740#57583931453631414E5A3331#{a5dcbf10-6530-11d2-901f-00c04fb951ed}
     DeviceDescription: USB Mass Storage Device
     PortPath:  0x2, 0x4, 0x0, 0x0, 0x0, 0x0
     All errors encountered:
   #1: (UsbHub3/173): SuperSpeed Device is Connected on the 2.0 Bus

   Record #3 (Key = 0x57ff79fd4e8)
     VendorID/ProductID: 0x1edb/0xbd3b
     PortPath:  0x3, 0x0, 0x0, 0x0, 0x0, 0x0
     All errors encountered:
   #1: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #2: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #3: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #4: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #5: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #6: (UsbHub3/176): DescriptorValidationErrorCompanionIsochEndpointWBytesPerIntervalTooLarge
   #7: (UsbHub3/176): DescriptorValidationErrorStringMismatchBetweenBlengthAndBufferLength
   #8: (UsbHub3/176): DescriptorValidationErrorStringMismatchBetweenBlengthAndBufferLength

   ```

   在前面的示例报表中，请注意**密钥**字段值为每个记录。 该报表根据那些对信息进行分类**密钥**值，以便更易读取。 相同**密钥**AllEvents.etl 中捕获的事件中使用的值。

4. 通过运行以下命令将 AllEvents.etl 转换为文本格式：

   ``` syntax
   USB3HWVerifierAnalyzer.exe -f AllEvents.etl /v > Output.txt 
   ```

   在输出文件中，搜索前面记下**密钥**值。 值与其中一个字段相关联： **fid\_UcxController**， **fid\_HubDevice**，以及**fid\_UsbDevice**.

5. 在网络监视器中，选择打开 AllEvents.etl**添加&lt;字段\_名称&gt;以显示筛选器**筛选由控制器、 中心和设备的事件。

## <a name="usb-hardware-verifier-flags"></a>USB 硬件验证程序标志


| Flag                                                | 表示将...                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DeviceHwVerifierClientInitiatedResetPipe            | 客户端驱动程序通过重置的 I/O 故障响应特定管道启动恢复操作。 某些客户端驱动程序可能在其他情况下执行错误恢复。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| DeviceHwVerifierClientInitiatedResetPort            | 客户端驱动程序通过重置以响应 I/O 故障设备启动恢复操作。 某些客户端驱动程序可能在其他情况下执行错误恢复。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| DeviceHwVerifierClientInitiatedCyclePort            | 客户端驱动程序由循环端口启动恢复操作。 此标志会导致要重新枚举设备的即插管理器。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| DeviceHwVerifierSetIsochDelayFailure                | USB 3.0 设备失败集\_ISOCH\_延迟请求。 设备可能会请求失败，因为该驱动程序不需要请求信息，或者发生了暂时性错误。 但是，该驱动程序无法区分这些原因。 在报表中未捕获此错误。                                                                                                                                                                                                                                                                                                                                                                                                                         |
| DeviceHwVerifierSetSelFailure                       | USB 3.0 设备失败集\_SEL 请求。 设备使用的请求信息的链接电源管理 (LPM)。 设备可能会请求失败，因为该驱动程序不需要请求信息，或者发生了暂时性错误。 但是，该驱动程序无法区分这些原因。 在报表中未捕获此错误。                                                                                                                                                                                                                                                                                                                                                         |
| DeviceHwVerifierSerialNumberMismatchOnRenumeration  | 该设备报告期间重新枚举而不是初始在枚举期间报告的一个不同的序列号。 重新枚举会导致重置端口或系统恢复操作发生。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| DeviceHwVerifierSuperSpeedDeviceWorkingAtLowerSpeed | USB 3.0 设备运行低于 SuperSpeed 总线速度。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| DeviceHwVerifierControlTransferFailure              | 控制传输到设备的默认终结点失败，失败。 传输可能会由于设备或控制器错误而失败。 中心日志指示传输失败的 USBD 状态代码。 此标志不包括集\_SEL 并设置\_ISOCH\_延迟控制传输失败。 DeviceHwVerifierSetIsochDelayFailure 和 DeviceHwVerifierSetSelFailure 标志包含在这些类型的请求。                                                                                                                                                                                                                                                                                                                |
| DeviceHwVerifierDescriptorValidationFailure         | 返回的设备的描述符不符合 USB 规范。 中心日志指示的确切错误。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| DeviceHwVerifierInterfaceWakeCapabilityMismatch     | RemoteWake 位未正确设置的设备中。 支持远程唤醒的 USB 3.0 设备还必须支持函数唤醒。 有两种方法中的设备将指示它对函数唤醒的支持。 第一种方法是通过**bmAttributes**配置描述符和第二种方法的字段位于其发送给 GET 响应\_状态请求定向到该接口。 对于非复合设备，RemoteWake 位值必须与 GET 返回的值匹配\_定向到接口 0 的状态请求。 对于复合设备，RemoteWake 位必须为 1 的至少一个函数。 否则，此标志指示该设备报告在这里相互矛盾的值。 |
| DeviceHwVerifierBusRenumeration                     | 设备将重新枚举总线上。 重新枚举会导致重置端口或系统恢复操作发生。 重新枚举也会发生，已禁用/启用或已停止/启动设备时。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| HubHwVerifierTooManyResets                          | 一个中心已经历过很多在短时间内重置操作。 虽然这些重置已成功，中心不处理请求而发生重复的错误。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| HubHwVerifierControlTransferFailure                 | 控制传输目标为中心的默认终结点失败。 传输可能会由于设备或控制器错误而失败。 中心日志指示失败的 USBD 状态代码。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| HubHwVerifierInterruptTransferFailure               | 数据传输到中心的中断终结点失败作为目标。 传输可能会由于设备或控制器错误而失败。 中心日志指示失败的 USBD 状态代码。 如果传输失败，因为请求已取消，不会捕获失败。                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| HubHwVerifierNoSelectiveSuspendSupport              | RemoteWake 位未设置为 1 的中心配置描述符中。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| HubHwVerifierPortResetTimeout                       | 在枚举或重新枚举设备时，端口重置操作超时。端口更改通知未收到指示端口重置已完成。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| HubHwVerifierInvalidPortStatus                      | 目标端口的端口状态无效，不能根据 USB 规范。 某些设备可能会导致中心报告无效的状态。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| HubHwVerifierPortLinkStateSSInactive                | 目标端口和下游设备之间的链接处于错误状态。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| HubHwVerifierPortLinkStateCompliance                | 目标端口和下游设备之间的链接是以兼容模式。 在某些情况下，涉及系统睡眠状态恢复，符合性模式错误，但在这些情况下不捕获失败。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| HubHwVerifierPortDeviceDisconnected                 | 目标端口上的下游设备无法再连接到总线。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| HubHwVerifierPortOverCurrent                        | 下游端口报告过电流状态。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| HubHwVerifierControllerOperationFailure             | 附加到目标端口的设备 （例如，启用设备，配置终结点） 的控制器操作失败。 组中的失败\_地址和重置终结点，请求不会捕获。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

 

## <a name="related-topics"></a>相关主题
[USB 诊断和测试指南](usb-driver-testing-guide.md)  



