---
description: '本主题介绍用于测试和调试特定硬件事件 ( # A0) 的 USB 硬件验证程序工具。'
title: USB 硬件验证程序 (USB3HWVerifierAnalyzer.exe)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b2ecf958358745db23ce90efb5973abae472c58
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968966"
---
# <a name="usb-hardware-verifier-usb3hwverifieranalyzerexe"></a>USB 硬件验证程序 (USB3HWVerifierAnalyzer.exe)


本主题介绍用于测试和调试特定硬件事件 ( # A0) 的 USB 硬件验证程序工具。

大多数硬件问题的原因是导致最终用户体验不佳，通常很难确定确切的故障。 USB 硬件验证器旨在捕获设备、端口、集线器、控制器或它们的组合中发生的硬件故障。

USB 硬件验证程序可以执行以下任务：

-   实时捕获硬件事件并显示信息。
-   生成包含所有事件相关信息的跟踪文件。
-   分析现有跟踪文件中的事件信息。

本主题包含以下各节：

-   [获取 USB 硬件验证器分析器工具](#getting-the-usb-hardware-verifier-analyzer-tool)
-   [如何使用 USB 硬件验证程序捕获事件](#how-to-capture-events-by-using-a-usb-hardware-verifier)
-   [USB 硬件验证程序标志](#usb-hardware-verifier-flags)

## <a name="getting-the-usb-hardware-verifier-analyzer-tool"></a>获取 USB 硬件验证器分析器工具


USB 硬件验证器工具随 MUTT 软件包一起提供，可从 [MUTT 软件包中的工具](mutt-software-package.md)下载。

"工具包" 包含多个工具，可执行压力和传输测试 (包括) 和 SuperSpeed 测试的电源转换。 此包还包含一个自述文档， (作为单独的下载) 提供。 本文档提供了有关 MUTT 硬件类型的简要概述。 它提供有关应运行的各种测试的分步指导，并为控制器、集线器、设备和 BIOS/UEFI 测试建议拓扑。

## <a name="how-to-capture-events-by-using-a-usb-hardware-verifier"></a>如何使用 USB 硬件验证程序捕获事件


若要使用硬件验证程序捕获事件，请执行以下步骤：

1. 通过在提升的命令提示符下运行此命令来启动会话。

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
   <th>说明</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td><p><a href="" id="---v--vendorid-"></a> -v &lt; VendorID&gt;</p></td>
   <td><p>记录指定的 VendorID 的所有硬件验证程序事件。</p></td>
   </tr>
   <tr class="even">
   <td><p><a href="" id="----p--productid-"></a> -p &lt; ProductID&gt;</p></td>
   <td><p>记录指定 ProductID 的所有硬件验证程序事件。</p></td>
   </tr>
   <tr class="odd">
   <td><p><a href="" id="-f--etl-file-"></a>-f &lt; ETL 文件&gt;</p></td>
   <td><p>分析指定的 ETL 文件。 不支持实时分析。 如果选择此选项，该工具会将文件脱机分析。</p></td>
   </tr>
   <tr class="even">
   <td><p>/v 输出</p></td>
   <td><p>向控制台显示所有事件。</p></td>
   </tr>
   </tbody>
   </table>

     

2. 运行要捕获其硬件事件的测试方案。

   在会话期间，USB 硬件验证器会在发生硬件事件时捕获有关这些事件的信息。 如果要筛选特定硬件的事件，请指定硬件的 VendorId 和产品 Id。 该工具可能不会捕获某些信息 (如 VID/PID) 有关设备完全枚举之前发生的事件的信息。 缺少的信息在会话结束时生成的详细报告中提供 (接下来的) 中所述。

   下面是硬件验证器工具的示例输出：

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

   会话结束时，将在当前目录中添加一个名为 AllEvents 的文件。 此文件包含有关在会话过程中捕获的所有事件的跟踪信息。

   除了 AllEvents，命令窗口还显示一个报表。 该报表包含实时输出中丢失的某些信息。 以下输出显示了上一个会话的示例测试报告。 该报表显示 USB 硬件验证程序遇到的所有事件。

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

   在上面的示例报表中，记下每个记录的 **键** 字段值。 报表按这些 **键值** 对信息进行分类，使其更易于阅读。 在 AllEvents 中捕获的事件中使用相同的 **密钥** 值。

4. 通过运行以下命令，将 AllEvents 转换为文本格式：

   ``` syntax
   USB3HWVerifierAnalyzer.exe -f AllEvents.etl /v > Output.txt 
   ```

   在输出文件中，搜索前面记下的 **键值** 。 这些值与以下其中一个字段相关联： **fid \_ UcxController**、 **fid \_ HubDevice**和 **fid \_ UsbDevice**。

5. 在 Netmon 中打开 AllEvents，选择 " **添加 &lt; 字段 \_ 名称" &gt; 以显示筛选** 器，按控制器、中心和设备筛选事件。

## <a name="usb-hardware-verifier-flags"></a>USB 硬件验证程序标志


| Flag                                                | 表示 .。。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| DeviceHwVerifierClientInitiatedResetPipe            | 客户端驱动程序通过在响应 i/o 故障时重置特定管道来启动恢复操作。 某些客户端驱动程序可能会在其他情况下执行错误恢复。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| DeviceHwVerifierClientInitiatedResetPort            | 客户端驱动程序通过在响应 i/o 故障时重置设备来启动恢复操作。 某些客户端驱动程序可能会在其他情况下执行错误恢复。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| DeviceHwVerifierClientInitiatedCyclePort            | 客户端驱动程序通过循环端口来启动恢复操作。 此标志会导致即插即用管理器重新枚举设备。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| DeviceHwVerifierSetIsochDelayFailure                | USB 3.0 设备未通过设置 \_ ISOCH \_ 延迟请求。 此设备可能会导致请求失败，原因是驱动程序不需要请求信息或发生暂时性错误。 但是，驱动程序无法区分这两个原因。 此错误不会在报表中捕获。                                                                                                                                                                                                                                                                                                                                                                                                                         |
| DeviceHwVerifierSetSelFailure                       | USB 3.0 设备未通过设置 \_ SEL 请求。 设备使用 (LPM) 的链接电源管理的请求信息。 此设备可能会导致请求失败，原因是驱动程序不需要请求信息或发生暂时性错误。 但是，驱动程序无法区分这两个原因。 此错误不会在报表中捕获。                                                                                                                                                                                                                                                                                                                                                         |
| DeviceHwVerifierSerialNumberMismatchOnRenumeration  | 设备在重新枚举期间报告了不同的序列号，而不是在初始枚举过程中报告的序列号。 重置端口或系统恢复操作可能会导致重新枚举。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| DeviceHwVerifierSuperSpeedDeviceWorkingAtLowerSpeed | USB 3.0 设备运行的总线速度低于 SuperSpeed。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| DeviceHwVerifierControlTransferFailure              | 未能将控件传输到设备的默认终结点。 由于设备或控制器错误，传输可能会失败。 中心日志表示传输失败的 USBD 状态代码。 此标志排除集 \_ SEL 并设置 \_ ISOCH \_ 延迟控制传输失败。 DeviceHwVerifierSetIsochDelayFailure 和 DeviceHwVerifierSetSelFailure 标志涵盖了这些类型的请求。                                                                                                                                                                                                                                                                                                                |
| DeviceHwVerifierDescriptorValidationFailure         | 设备返回的描述符不符合 USB 规范。 集线器日志指示确切的错误。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| DeviceHwVerifierInterfaceWakeCapabilityMismatch     | 设备中错误地设置了 RemoteWake 位。 支持远程唤醒的 USB 3.0 设备还必须支持函数唤醒。 设备提供了两种方法来指示其函数唤醒支持。 第一种方法是通过配置描述符的 **bmAttributes** 字段，第二种方法是响应 \_ 针对接口的 GET 状态请求。 对于非复合设备，RemoteWake 位值必须与 GET STATUS 请求返回的值（ \_ 针对接口0）匹配。 对于复合设备，对于至少一个函数，RemoteWake 位必须为1。 否则，此标志表明设备在此处报告了矛盾的值。 |
| DeviceHwVerifierBusRenumeration                     | 在总线上重新枚举设备。 重置端口或系统恢复操作可能会导致重新枚举。 当禁用/启用或停止/启动设备时，也会发生重新枚举。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| HubHwVerifierTooManyResets                          | 某个集线器在一小段时间内经历了太多的重置操作。 即使这些重置成功，集线器也不处理请求，并发生重复错误。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| HubHwVerifierControlTransferFailure                 | 针对中心默认终结点的控件传输失败。 由于设备或控制器错误，传输可能会失败。 中心日志表示失败的 USBD 状态代码。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| HubHwVerifierInterruptTransferFailure               | 针对中心中断终结点的数据传输失败。 由于设备或控制器错误，传输可能会失败。 中心日志表示失败的 USBD 状态代码。 如果由于请求已取消而导致传输失败，则不会捕获失败。                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| HubHwVerifierNoSelectiveSuspendSupport              | 中心配置描述符中的 RemoteWake 位未设置为1。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| HubHwVerifierPortResetTimeout                       | 枚举或重新枚举设备时，端口重置操作会超时。未收到指示端口重置完成的端口更改通知。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| HubHwVerifierInvalidPortStatus                      | 根据 USB 规范，目标端口的端口状态无效。 某些设备可能会导致集线器报告无效状态。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| HubHwVerifierPortLinkStateSSInactive                | 目标端口和下游设备之间的链接处于错误状态。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| HubHwVerifierPortLinkStateCompliance                | 目标端口和下游设备之间的链接处于符合性模式。 在某些涉及系统睡眠恢复的情况下，符合性模式错误是预期的，在这种情况下，不会捕获故障。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| HubHwVerifierPortDeviceDisconnected                 | 目标端口上的下游设备不再连接到总线。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| HubHwVerifierPortOverCurrent                        | 下游端口报告了过流状态。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| HubHwVerifierControllerOperationFailure             | 控制器操作 (例如，启用设备，为连接到目标端口的设备配置终结点) 失败。 \_不会捕获设置地址和重置终结点请求中的失败。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

 

## <a name="related-topics"></a>相关主题
[USB 诊断和测试指南](usb-driver-testing-guide.md)  



