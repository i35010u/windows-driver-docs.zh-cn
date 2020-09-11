---
description: 本主题列出了 USB 驱动程序文档集中的 "操作方法" 主题。 每个操作说明主题提供一组任务作为一系列包含代码示例的步骤。
title: USB 客户端驱动程序的常见任务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 183996041405f2915076f3aeed8b7e3b88ec6adb
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010465"
---
# <a name="common-tasks-for-usb-client-drivers"></a>USB 客户端驱动程序的常见任务


本主题列出了本文档集中的 "操作方法" 主题。 每个操作说明主题提供一组任务作为一系列包含代码示例的步骤。

"如何" 主题提供有关与 USB 客户端驱动程序任务相关的过程的分步说明。 通常情况下，这些主题的编写假设你要扩展 Microsoft Visual Studio 2012 附带的 USB 模板创建的驱动程序。

此列表包含指向 USB 客户端驱动程序的操作指南主题的链接。

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
<td><p>在本主题中，你将使用随 Microsoft Visual Studio 11 专业测试版提供的 USB 内核模式驱动程序模板来编写简单的内核模式驱动程序框架 (基于 KMDF) 的客户端驱动程序。 生成和安装客户端驱动程序后，你将在设备管理器中查看客户端驱动程序，并在调试器中查看驱动程序输出。</p></td>
</tr>
<tr class="even">
<td><p><a href="implement-driver-entry-for-a-usb-driver--umdf-.md" data-raw-source="[How to write your first USB client driver (UMDF)](implement-driver-entry-for-a-usb-driver--umdf-.md)">如何编写第一个 USB 客户端驱动程序 (UMDF)</a></p></td>
<td><p>在本主题中，你将使用随 Microsoft Visual Studio 11 Beta 版提供的 USB 用户模式驱动程序模板来编写基于 (UMDF) 的客户端驱动程序的用户模式驱动程序框架。 生成和安装客户端驱动程序后，你将在设备管理器中查看客户端驱动程序，并在调试器中查看驱动程序输出。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-configuration-descriptors.md" data-raw-source="[How to get the configuration descriptor](usb-configuration-descriptors.md)">如何获取配置描述符</a></p></td>
<td><p>本主题介绍了配置的重要字段，并包含有关如何从 USB 设备获取配置描述符的分步指导。</p></td>
</tr>
<tr class="even">
<td><p><a href="send-requests-to-the-usb-driver-stack.md" data-raw-source="[How to Submit an URB (WDM)](send-requests-to-the-usb-driver-stack.md)">如何将 URB (WDM 提交) </a></p></td>
<td><p>本主题介绍将已初始化的 URB 提交到 USB 驱动程序堆栈以处理特定请求所需的步骤。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">如何选择 USB 设备的配置</a></p></td>
<td><p>在本主题中，你将了解如何在通用串行总线 (USB) 设备中选择配置。 本主题介绍通过提交 URB 发送选择配置请求的过程。</p></td>
</tr>
<tr class="even">
<td><p><a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">如何在 USB 界面中选择备用设置</a></p></td>
<td><p>本主题介绍发出选择接口请求以激活 USB 接口中的替代设置的步骤。 在选择 USB 配置之后，客户端驱动程序必须发出此请求。 默认情况下，选择配置还会激活该配置的每个接口中的第一个备用设置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-get-usb-pipe-handles.md" data-raw-source="[How to enumerate USB pipes](how-to-get-usb-pipe-handles.md)">如何枚举 USB 管道</a></p></td>
<td><p>本主题概述了 USB 管道，并介绍了 USB 客户端驱动程序从 USB 驱动程序堆栈获取管道句柄所需的步骤。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">如何使用连续读取器从 USB 管道读取数据</a></p></td>
<td><p>本主题介绍 WDF 提供的连续读取器对象。 本主题中的过程提供了有关如何配置对象并使用它从 USB 管道读取数据的分步说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">如何发送 USB 控制传输</a></p></td>
<td><p>本主题介绍控制传输的结构以及客户端驱动程序应如何将控制请求发送到设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to transfer data to USB bulk endpoints](usb-bulk-and-interrupt-transfer.md)">如何将数据传输到 USB 批量终结点</a></p></td>
<td><p>本主题提供有关 USB 批量传输的简要概述。 它还提供了有关客户端驱动程序如何从设备发送和接收大容量数据的分步说明。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to open and close static streams in a USB bulk endpoint](how-to-open-streams-in-a-usb-endpoint.md)">如何打开和关闭 USB 大容量终结点中的静态流</a></p></td>
<td><p>本主题讨论静态流功能，并说明 USB 客户端驱动程序如何在 USB 3.0 设备的大容量终结点中打开和关闭流。</p></td>
</tr>
<tr class="even">
<td><p><a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">如何将数据传输到 USB 常时等量终结点</a></p></td>
<td><p>本主题介绍客户端驱动程序如何构建 USB 请求块 (URB) 将数据传入和传出 USB 设备中受支持的同步终结点。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-recover-from-usb-pipe-errors.md" data-raw-source="[How to recover from USB pipe errors](how-to-recover-from-usb-pipe-errors.md)">如何从 USB 管道错误中恢复</a></p></td>
<td><p>本主题提供有关在将数据传输到 USB 管道失败时可尝试执行的步骤的信息。 本主题中所述的机制介绍了对批量、中断和同步管道的中止、重置和循环端口操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-chained-mdls.md" data-raw-source="[How to send chained MDLs](how-to-send-chained-mdls.md)">如何发送链接的 MDL</a></p></td>
<td><p>在本主题中，你将了解有关 USB 驱动程序堆栈中链式 MDLs 功能的信息，以及客户端驱动程序如何以 MDL 结构链形式发送传输缓冲区。</p></td>
</tr>
<tr class="odd">
<td><p><a href="register-a-composite-driver.md" data-raw-source="[How to Register a Composite Device](register-a-composite-driver.md)">如何注册复合设备</a></p></td>
<td><p>本主题介绍了称为复合驱动程序的 USB 多功能设备的驱动程序如何使用基础 USB 驱动程序堆栈注册和注销复合设备。 Microsoft 提供的驱动程序 Usbccgp.sys 是 Windows 加载的默认复合驱动程序。 本主题中的过程适用于自定义 Windows 驱动模型基于 (WDM) 的复合驱动程序，该驱动程序将替换 Usbccgp.sys。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to--implement-remote-and-function-wake-support.md" data-raw-source="[How to Implement Function Suspend in a Composite Driver](how-to--implement-remote-and-function-wake-support.md)">如何在复合驱动程序中实现函数挂起</a></p></td>
<td><p>本主题概述了适用于通用串行总线的函数挂起和函数远程唤醒功能 (USB) 3.0 多功能设备 (复合设备) 。 在本主题中，你将了解如何在控制复合设备的驱动程序中实现这些功能。 本主题适用于替换 Usbccgp.sys 的复合驱动程序。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[ (USB) 驱动程序的通用串行总线](../index.yml)