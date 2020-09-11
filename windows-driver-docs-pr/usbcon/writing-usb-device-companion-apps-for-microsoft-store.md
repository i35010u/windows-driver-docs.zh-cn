---
description: Windows. u 命名空间提供 Api 以与外部 USB 设备进行通信。
title: USB 设备的 UWP 应用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b96e0680bbf3bd674d18e4a6230d55519d13c4a
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010361"
---
# <a name="uwp-app-for-a-usb-device"></a>USB 设备的 UWP 应用


Windows [**应用**](/uwp/api/Windows.Devices.Usb) 程序提供了一种方法，用于与使用 WinUSB ( # A0) 作为设备驱动程序的外部 Usb 设备进行通信。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="talking-to-usb-devices-start-to-finish.md" data-raw-source="[Talking to USB devices, start to finish (UWP app)](talking-to-usb-devices-start-to-finish.md)">与 USB 设备通信，从开始到完成（UWP 应用）</a></p></td>
<td><p>使用 Windows 8.1 中引入的 Windows 运行时 Api 编写允许用户访问其外围设备 USB 设备的 UWP 应用。 此类应用程序可以基于用户指定的条件连接到设备、获取有关设备的信息、将数据发送到设备，反之亦然地从设备中获取数据流，以及轮询设备是否有中断数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="updating-the-app-manifest-with-usb-device-capabilities.md" data-raw-source="[How to add USB device capabilities to the app manifest](updating-the-app-manifest-with-usb-device-capabilities.md)">如何将 USB 设备功能添加到应用部件清单</a></p></td>
<td><p>本主题介绍使用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb)"><strong>Windows Usb</strong></a> 命名空间的 windows 应用程序所需的设备功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">如何连接到 USB 设备（UWP 应用）</a></p></td>
<td><p>在 Windows 8.1 中，可以编写与 USB 设备交互的 UWP 应用。 应用可以发送控制命令、获取设备信息，以及在大容量和中断终结点之间读取和写入数据。 在执行所有这些操作之前，必须找到设备并建立连接。</p>
<p>在此部分中，你将了解如何使用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.DeviceWatcher" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](/uwp/api/Windows.Devices.Enumeration.DeviceWatcher)"><strong>DeviceWatcher</strong></a> 对象查找设备，然后打开该设备，开始从你的应用进行通信。 你还将了解如何在使用完设备后关闭设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">如何发送 USB 控制传输（UWP 应用）</a></p></td>
<td><p>与 USB 设备通信的应用通常会发送多个控制传输请求。 这些请求将获取硬件供应商定义的设备和发送控制命令的相关信息。 在本主题中，你将了解如何进行控件传输，以及如何在 UWP 应用中设置其格式并发送它们。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-send-a-usb-interrupt-transfer--uwp-app-.md" data-raw-source="[How to send a USB interrupt transfer request (UWP app)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)">如何发送 USB 中断传输请求（UWP 应用）</a></p></td>
<td><p>USB 设备可以支持中断终结点，以便它可以定期发送或接收数据。 为实现此目的，主机会定期轮询设备，并在每次主机轮询设备时传输数据。 中断传输主要用于从设备获取中断数据。 本主题介绍 UWP 应用如何从设备获取连续中断数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">如何将发送 USB 大容量传输请求（UWP 应用）</a></p></td>
<td><p>在本主题中，你将了解有关 USB 批量传输的信息，以及如何从 UWP 应用启动与 USB 设备通信的传输请求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">如何获取 USB 描述符（UWP 应用）</a></p></td>
<td><p>与 USB 设备交互的主要任务之一就是获取相关信息。 所有 USB 设备都以几个称为描述符的数据结构形式提供信息。 本主题介绍 UWP 应用如何从设备上的终结点、接口、配置和设备级别获取描述符。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">如何选择 USB 接口设置（UWP 应用）</a></p></td>
<td><p>在本主题中，你将了解如何更改 USB 接口内的设置。 你将使用 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting&lt;/strong&gt;](/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting)"><strong>UsbInterfaceSetting</strong></a> 对象获取当前设置并在接口中设置设置。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-samples"></a>USB 示例


-   [自定义 USB 设备访问示例](https://go.microsoft.com/fwlink/p/?linkid=309716)
-   [USB CDC 控制示例](https://go.microsoft.com/fwlink/p/?linkid=309716)
-   [固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?linkid=309716)

## <a name="what-are-the-limitations-of-the-namespace"></a>命名空间的限制是什么？


在这些情况下， *不能* 使用 [**Windows. Usb**](/uwp/api/Windows.Devices.Usb) ：

-   如果未 Winusb.sys 设备驱动程序。
-   要与设备的 USB 同步终结点进行通信。
-   你要传递 SuperSpeed 大容量终结点的流。 对于这些终结点，用于大容量传输的 USB Windows 运行时类只能发送或接收来自终结点的第一个流的数据。
-   允许多个应用同时访问设备。
-   USB 设备是一个内部设备。
    **注意**   Api 主要用于访问外围设备。 该 API 还可以访问 PC 内部 USB 设备。 但是，从 UWP 应用访问 PC 内部 USB 设备的权限仅限于 OEM 为该 PC 显式声明的特权应用。

     

-   内核模式设备堆栈 Winusb.sys 上有一个筛选器驱动程序。
    **注意**   此方案仅适用于特权应用。

     

-   你的设备有多个 USB 配置，并且你想要选择除第一个以外的配置。 默认情况下， [**Windows 设备。**](/uwp/api/Windows.Devices.Usb)

## <a name="related-topics"></a>相关主题
[**Windows.Devices.Usb**](/uwp/api/Windows.Devices.Usb)