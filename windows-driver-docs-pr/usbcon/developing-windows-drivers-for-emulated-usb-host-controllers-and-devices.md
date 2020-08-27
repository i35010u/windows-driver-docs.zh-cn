---
description: 开发模拟 USB 设备 (UDE) 的 Windows 驱动程序的概述
title: 开发模拟 USB 设备 (UDE) 的 Windows 驱动程序的概述
ms.date: 10/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3f6ddcfa0229ef2bcc860c117a595181b94beeff
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969086"
---
# <a name="overview-of-developing-windows-drivers-for-emulated-usb-devices-ude"></a>开发模拟 USB 设备 (UDE) 的 Windows 驱动程序的概述


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>本部分介绍 Windows 操作系统中 (UDE) 支持的 USB 模拟设备，用于开发模拟通用串行总线 (USB) 主机控制器驱动程序和连接的虚拟 USB 设备。 这两个组件组合成单个 KMDF 驱动程序，该驱动程序可以与 Microsoft 提供的 USB 设备模拟类扩展 (UdeCx) 通信。</p>
<p><strong>开发工具和 Microsoft 提供的二进制文件</strong></p>
<p>Windows 驱动程序工具包 (WDK) 包含开发驱动程序所需的资源，如头文件、库、工具和示例。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">下载适用于 Windows 的工具包和工具</a></p>
<p>若要编写函数控制器驱动程序，需要：</p>
<ul>
<li>UdeCx： ( # A0) 函数驱动程序使用的 WDF 扩展。 此扩展包含在 Windows 中。</li>
<li>链接到存根库 (Udecxstub) 。 该存根库在 WDK 中。</li>
<li>在 WDK 中包括 Udecx。</li>
</ul>
<p><strong>版本历史记录</strong></p>
<p></p>
<dl>
<dt><a href=""></a>Windows 10</dt>
<dd><p>UDE 版本1.0。</p>
<p>KMDF 版本1.15。</p>
<p>不支持 UMDF。</p>
</dd>
</dl></td>
<td><p><strong>UDE 的体系结构</strong></p>
<a href="usb-emulated-device--ude--architecture.md" data-raw-source="[Architecture: USB Device Emulation (UDE)](usb-emulated-device--ude--architecture.md)">体系结构： Usb 设备仿真 (UDE) </a>Windows 中的
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers](usb-3-0-driver-stack-architecture.md)">usb 主机端驱动程序</a>
<p><strong>为模拟主机控制器和设备编写驱动程序</strong></p>
<p>熟悉 UDE 对象和句柄。 有关 WDF 对象的详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects" data-raw-source="[Introduction to Framework Objects](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)">框架对象简介</a>。</p>
<p>了解 UDE 的行为，该行为与客户端驱动程序交互的方式以及客户端驱动程序应实现的功能。</p>
<p><a href="writing-a-ude-client-driver.md" data-raw-source="[Write a UDE client driver](writing-a-ude-client-driver.md)">编写 UDE 客户端驱动程序</a></p>
<p><strong>编程参考节</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#emulated-host-controller-driver-reference" data-raw-source="[Emulated USB host controller driver programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#emulated-host-controller-driver-reference)">Emulated USB host controller driver programming reference</a>（模拟 USB 主控制器驱动程序编程参考）</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/" data-raw-source="[WDF Reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf/)">WDF 引用</a></p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/usbcon)  



