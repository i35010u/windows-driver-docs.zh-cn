---
Description: 本主题列出了"如何"主题中的 USB 驱动程序文档集。 每个操作方法主题显示一组任务的步骤序列，并且带有代码示例。
title: USB 客户端驱动程序的常见任务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ae8bf2cd77c58138cda95df8ef448e50f0ca2fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356550"
---
# <a name="common-tasks-for-usb-client-drivers"></a>USB 客户端驱动程序的常见任务


本主题列出了"如何"主题，本文档集中。 每个操作方法主题显示一组任务的步骤序列，并且带有代码示例。

如何主题为您提供有关与 USB 客户端驱动程序任务相关的进程的分步说明。 通常情况下，主题扩展由 Microsoft Visual Studio 2012 中附带的 USB 模板创建的驱动程序的假设编写。

此列表包含 USB 客户端驱动程序的操作指南主题的链接。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>任务</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="tutorial--write-your-first-usb-client-driver--kmdf-.md" data-raw-source="[How to write your first USB client driver (KMDF)](tutorial--write-your-first-usb-client-driver--kmdf-.md)">如何编写第一个 USB 客户端驱动程序 (KMDF)</a></p></td>
<td><p>本主题中你将使用随 Microsoft Visual Studio 11 Professional Beta 提供的 USB 内核模式驱动程序模板编写简单的内核模式驱动程序框架 (KMDF) 的基于客户端驱动程序。 生成和安装客户端驱动程序后, 将在设备管理器中查看客户端驱动程序并在调试器中查看驱动程序输出。</p></td>
</tr>
<tr class="even">
<td><p><a href="implement-driver-entry-for-a-usb-driver--umdf-.md" data-raw-source="[How to write your first USB client driver (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)">如何编写第一个 USB 客户端驱动程序 (UMDF)</a></p></td>
<td><p>本主题中将提供使用 Microsoft Visual Studio 11 Beta 的 USB 用户模式驱动程序模板编写用户模式驱动程序框架 (UMDF) 的基于客户端驱动程序。 生成和安装客户端驱动程序后, 将在设备管理器中查看客户端驱动程序并在调试器中查看驱动程序输出。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-configuration-descriptors.md" data-raw-source="[How to get the configuration descriptor](usb-configuration-descriptors.md)">如何获取配置描述符</a></p></td>
<td><p>本主题介绍了配置的重要字段并包括有关如何获取配置描述符从 USB 设备的分步指南。</p></td>
</tr>
<tr class="even">
<td><p><a href="send-requests-to-the-usb-driver-stack.md" data-raw-source="[How to Submit an URB (WDM)](send-requests-to-the-usb-driver-stack.md)">如何提交 URB (WDM)</a></p></td>
<td><p>本主题介绍提交初始化的 URB USB 驱动程序堆栈处理特定请求所需的步骤。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何选择 USB 设备的配置</a></p></td>
<td><p>在本主题中，将了解如何在通用串行总线 (USB) 设备中选择一个配置。 本主题介绍通过提交 URB 发送选择的配置请求的过程。</p></td>
</tr>
<tr class="even">
<td><p><a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">如何在 USB 界面中选择一项备用设置</a></p></td>
<td><p>本主题介绍发出选择接口请求以激活一项备用设置 USB 接口中的步骤。 客户端驱动程序必须选择 USB 配置后发出此请求。 默认情况下，选择一个配置，还会激活该配置中每个接口中的第一个备用设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-get-usb-pipe-handles.md" data-raw-source="[How to enumerate USB pipes](how-to-get-usb-pipe-handles.md)">如何枚举 USB 管道</a></p></td>
<td><p>本主题概述了 USB 管道，并介绍了通过 USB 客户端驱动程序从 USB 驱动程序堆栈获取管道句柄所必需的步骤。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">如何使用来从 USB 管道读取数据的连续读取器</a></p></td>
<td><p>本主题介绍 WDF 提供持续的读取器对象。 本主题中的过程提供有关如何配置对象并使用它从 USB 管道读取数据的分步说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">如何发送 USB 控制传输</a></p></td>
<td><p>本主题介绍控制传输和如何客户端驱动程序应将控制请求发送到设备的结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to transfer data to USB bulk endpoints](usb-bulk-and-interrupt-transfer.md)">如何将数据传输到 USB 大容量终结点</a></p></td>
<td><p>本主题提供有关 USB 批量传输的简要概述。 它还提供有关如何对客户端驱动程序可以发送和接收来自设备的大容量数据的分步说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to open and close static streams in a USB bulk endpoint](how-to-open-streams-in-a-usb-endpoint.md)">如何打开和关闭 USB 大容量终结点中的静态流</a></p></td>
<td><p>本主题讨论了静态流功能并说明如何打开和关闭的流，大容量的 USB 3.0 设备终结点中 USB 客户端驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">如何将数据传输到 USB 等时终结点</a></p></td>
<td><p>本主题介绍客户端驱动程序可以如何生成 USB 请求块 (URB) 将在 USB 设备中受支持等时终结点的数据传输。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-recover-from-usb-pipe-errors.md" data-raw-source="[How to recover from USB pipe errors](how-to-recover-from-usb-pipe-errors.md)">如何从 USB 管道错误中恢复</a></p></td>
<td><p>本主题提供有关步骤的信息可以尝试在数据传输到 USB 管道时失败。 本主题涵盖中所述的机制中止，重置，并循环大容量、 中断，并等时管道上的端口操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">如何发送链接 MDLs</a></p></td>
<td><p>在本主题中，您将学习有关 USB 驱动程序堆栈，以及客户端驱动程序如何作为 MDL 结构链发送的传输缓冲区中的链接 MDLs 功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="register-a-composite-driver.md" data-raw-source="[How to Register a Composite Device](register-a-composite-driver.md)">如何注册的复合设备</a></p></td>
<td><p>本主题介绍如何称为复合驱动程序，USB 多功能设备的驱动程序可以注册和注销的复合设备与基础的 USB 驱动程序堆栈。 Microsoft 提供驱动程序，Usbccgp.sys，是由 Windows 加载默认复合驱动程序。 本主题中的过程适用于自定义 Windows 驱动程序模型 WDM 基于复合驱动程序，用于替换 Usbccgp.sys。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to--implement-remote-and-function-wake-support.md" data-raw-source="[How to Implement Function Suspend in a Composite Driver](how-to--implement-remote-and-function-wake-support.md)">如何实现复合的驱动程序中函数挂起</a></p></td>
<td><p>本主题提供的函数概述挂起和函数远程唤醒功能的通用串行总线 (USB) 3.0 的多功能设备 （复合设备）。 本主题中将学习如何在控制复合设备的驱动程序中实现这些功能。 本主题适用于复合替换 Usbccgp.sys 的驱动程序。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB) 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/)  



