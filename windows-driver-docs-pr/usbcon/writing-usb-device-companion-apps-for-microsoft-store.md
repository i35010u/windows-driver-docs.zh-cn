---
Description: Windows.Devices.Usb 命名空间提供 Api 以便与外部 USB 设备进行通信。
title: USB 设备的 UWP 应用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30bde1de66ca92298e34c272d2c8ddca339eac1e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389107"
---
# <a name="uwp-app-for-a-usb-device"></a>USB 设备的 UWP 应用


[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)命名空间提供与使用 WinUSB (Winusb.sys) 作为设备驱动程序的外部 USB 设备进行通信的 Windows 应用一种方法。

## <a name="in-this-section"></a>本节内容


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
<td><p><a href="talking-to-usb-devices-start-to-finish.md" data-raw-source="[Talking to USB devices, start to finish (UWP app)](talking-to-usb-devices-start-to-finish.md)">与 USB 设备通信，启动以完成 （UWP 应用）</a></p></td>
<td><p>在 Windows 8.1 中引入的 Windows 运行时 Api 用于编写允许用户访问其外围的 USB 设备的 UWP 应用。 此类应用程序可以连接到基于用户指定的条件的设备、 获取有关设备的信息、 将数据发送到设备和与之相反获取数据会从该设备，并轮询中断数据的设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="updating-the-app-manifest-with-usb-device-capabilities.md" data-raw-source="[How to add USB device capabilities to the app manifest](updating-the-app-manifest-with-usb-device-capabilities.md)">如何将 USB 设备功能添加到应用程序清单</a></p></td>
<td><p>本主题介绍使用 Windows 应用所需的设备功能<a href="https://msdn.microsoft.com/library/windows/apps/dn278466" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278466)"> <strong>Windows.Devices.Usb</strong> </a>命名空间。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">如何连接到 USB 设备 （UWP 应用）</a></p></td>
<td><p>在 Windows 8.1，可以编写与 USB 设备进行交互的 UWP 应用。 应用可以发送控制命令，获取设备的信息，并读取和写入数据传入/传出大容量和中断终结点。 您可以执行所有这些之前，必须找到设备，并建立连接。</p>
<p>在此部分中，您将学习如何使用<a href="https://msdn.microsoft.com/library/windows/apps/br225446" data-raw-source="[&lt;strong&gt;DeviceWatcher&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/br225446)"> <strong>DeviceWatcher</strong> </a>对象找到该设备，然后打开它开始从您的应用程序进行通信。 您将学习如何使用它完成后关闭设备。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">如何发送 USB 控制传输 （UWP 应用）</a></p></td>
<td><p>通常与 USB 设备进行通信的应用将请求发送多个控制传输。 这些请求获取有关设备的信息并发送由硬件供应商定义的控制命令。 本主题中介绍有关控制传输以及如何设置格式并将其发送在 UWP 应用中。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-send-a-usb-interrupt-transfer--uwp-app-.md" data-raw-source="[How to send a USB interrupt transfer request (UWP app)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)">如何发送 USB 中断传输请求 （UWP 应用）</a></p></td>
<td><p>USB 设备可以支持中断终结点，以便它可以发送或接收的数据按固定间隔。 若要完成此操作，主机轮询设备按固定间隔和传输主机轮询设备每次数据。 中断传送主要用于从设备获取中断数据。 本主题介绍如何为 UWP 应用可以从设备获取持续中断数据。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">如何将发送的 USB 大容量传输请求 （UWP 应用）</a></p></td>
<td><p>在本主题中，您将了解 USB 大容量传输，以及如何启动 UWP 应用中所使用的 USB 设备进行通信的传输请求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">如何获取 USB 描述符 （UWP 应用）</a></p></td>
<td><p>一个与 USB 设备进行交互的主要任务是获取有关它的信息。 所有 USB 设备都提供的多个数据结构称为描述符窗体中的信息。 本主题介绍如何为 UWP 应用可以从终结点、 接口、 配置和设备级别的设备获取描述符。</p></td>
</tr>
<tr class="even">
<td><p><a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">如何选择 USB 接口设置 （UWP 应用）</a></p></td>
<td><p>在本主题中，您将学习如何更改 USB 接口内的设置。 将使用<a href="https://msdn.microsoft.com/library/windows/apps/dn264278" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264278)"> <strong>UsbInterfaceSetting</strong> </a>对象来获取当前设置，并在界面中设置的设置。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-samples"></a>USB 示例


-   [自定义的 USB 设备访问示例](https://go.microsoft.com/fwlink/p/?linkid=309716)
-   [USB CDC 控制示例](https://go.microsoft.com/fwlink/p/?linkid=309716)
-   [固件更新 USB 设备示例](https://go.microsoft.com/fwlink/p/?linkid=309716)

## <a name="what-are-the-limitations-of-the-namespace"></a>命名空间的限制是什么？


您*不能*使用[ **Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)在这些情况下：

-   如果设备驱动程序不是 Winusb.sys。
-   你想要与 USB 设备的同步终结点通信。
-   你想要进行通信的 SuperSpeed 大容量终结点的流。 对于这些终结点，大容量传输的 USB Windows 运行时类只能发送或接收终结点的第一个流的数据。
-   允许多个应用程序能够同时访问设备。
-   USB 设备是内部的设备。
    **请注意**   Api 的主要设计用于访问外围设备。 API 还可以访问 PC 内部的 USB 设备。 但是从 UWP 应用到 PC 内部的 USB 设备的访问权限仅限于该电脑的显式声明由 OEM 的特权应用程序。

     

-   内核模式设备堆栈具有 Winusb.sys 上面的筛选器驱动程序。
    **请注意**  此方案可供特权的应用。

     

-   你的设备有多个 USB 配置，并且你想要选择第一个以外的配置。 [**Windows.Devices.Usb** ](https://msdn.microsoft.com/library/windows/apps/dn278466)默认情况下选择的第一个配置。

## <a name="related-topics"></a>相关主题
[**Windows.Devices.Usb**](https://msdn.microsoft.com/library/windows/apps/dn278466)  



