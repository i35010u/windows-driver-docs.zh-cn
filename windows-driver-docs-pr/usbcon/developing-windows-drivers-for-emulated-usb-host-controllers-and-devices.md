---
Description: 开发模拟 USB 设备 (UDE) 的 Windows 驱动程序
title: 开发模拟 USB 设备 (UDE) 的 Windows 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b36a2057ea3a8ab84023ef2bfa96e830d28f5d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377415"
---
# <a name="developing-windows-drivers-for-emulated-usb-devices-ude"></a>开发模拟 USB 设备 (UDE) 的 Windows 驱动程序


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>用途</strong></p>
<p>本部分介绍 Windows 操作系统中，为开发模拟通用串行总线 (USB) 主机控制器驱动程序和连接的虚拟 USB 设备的模拟的 USB 设备 (UDE) 支持。 这两个组件组合成单个 KMDF 驱动程序，该驱动程序可以与 Microsoft 提供的 USB 设备模拟类扩展 (UdeCx) 通信。</p>
<p><strong>开发工具和 Microsoft 提供的二进制文件</strong></p>
<p>Windows Driver Kit (WDK) 包含所需的驱动程序开发，例如标头、 库、 工具和示例的资源。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">下载适用于 Windows 的工具包和工具</a></p>
<p>若要编写函数控制器驱动程序，需要：</p>
<ul>
<li>UdeCx: (udecx.sys) WDF 扩展由功能驱动程序。 此扩展插件包括在 Windows 中。</li>
<li>链接到存根 （stub） 库 (Udecxstub.lib)。 存根 （stub） 库是在 WDK 中。</li>
<li>包括 Udecx.h WDK 中提供。</li>
</ul>
<p><strong>版本历史记录</strong></p>
<p></p>
<dl>
<dt><a href=""></a>Windows 10</dt>
<dd><p>UDE 1.0 版。</p>
<p>KMDF 1.15 版。</p>
<p>不支持 UMDF。</p>
</dd>
</dl></td>
<td><p><strong>UDE 的体系结构</strong></p>
<a href="usb-emulated-device--ude--architecture.md" data-raw-source="[Architecture: USB Device Emulation (UDE)](usb-emulated-device--ude--architecture.md)">体系结构：USB 设备仿真 (UDE)</a>
<a href="usb-3-0-driver-stack-architecture.md" data-raw-source="[USB host-side drivers](usb-3-0-driver-stack-architecture.md)">USB 宿主端驱动程序</a>在 Windows 中
<p><strong>编写仿真的主机控制器和设备驱动程序</strong></p>
<p>熟悉 UDE 对象和句柄。 WDF 对象的详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff544249" data-raw-source="[Introduction to Framework Objects](https://msdn.microsoft.com/library/windows/hardware/ff544249)">Framework 对象简介</a>。</p>
<p>了解行为的 UDE，它与客户端驱动程序，以及客户端驱动程序的功能交互的方式应实现。</p>
<p><a href="writing-a-ude-client-driver.md" data-raw-source="[Write a UDE client driver](writing-a-ude-client-driver.md)">编写 UDE 客户端驱动程序</a></p>
<p><strong>编程参考节</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#emulated-host-controller-driver-reference" data-raw-source="[Emulated USB host controller driver programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#emulated-host-controller-driver-reference)">Emulated USB host controller driver programming reference</a>（模拟 USB 主控制器驱动程序编程参考）</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265590" data-raw-source="[WDF Reference](https://msdn.microsoft.com/library/windows/hardware/dn265590)">WDF 引用</a></p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



