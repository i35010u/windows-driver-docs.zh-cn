---
Description: 为 USB 功能控制器开发 Windows 驱动程序的概述
title: 为 USB 功能控制器开发 Windows 驱动程序的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fae4e4aacb28a1cb4ec4b665c0e4cd7c2d3b7e5a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842392"
---
# <a name="overview-of-developing-windows-drivers-for-usb-function-controllers"></a>为 USB 功能控制器开发 Windows 驱动程序的概述


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>用途</strong></p>
<p>本部分介绍 Windows 操作系统中的支持，用于开发与 Microsoft 提供的 USB 函数控制器扩展（UFX）通信的通用串行总线（USB）函数控制器驱动程序。</p>
<p><strong>开发工具和 Microsoft 提供的二进制文件</strong></p>
<p>Windows 驱动程序工具包（WDK）包含驱动程序开发所需的资源，如标头、库、工具和示例。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">下载适用于 Windows 的工具包和工具</a></p>
<p>若要编写函数控制器驱动程序，需要：</p>
<ul>
<li>UFX （Ufx01000）已加载为 FDO。 此驱动程序包含在 Windows 中。</li>
<li>指向存根库（Ufx01000）的链接。 该存根库在 WDK 中。 库转换由函数控制器驱动程序发出的调用，并将其传递给 UFX。</li>
<li>在 WDK 中包括 Ufxclient。</li>
</ul>
<p>若要从用户模式发送请求，需要：</p>
<ul>
<li>GenericUSBFn 加载为 USB 函数类驱动程序。 此驱动程序包含在 Windows 中。</li>
<li>在 WDK 中包括 Genericusbfnioctl。</li>
</ul>
<p>若要从 USB 类驱动程序发送请求，需要：</p>
<ul>
<li>UFX （Ufx01000）已加载为 FDO。 此驱动程序包含在 Windows 中。</li>
<li>在 WDK 中包括 Usbfnioctl。</li>
</ul>
若要编写一个筛选器驱动程序来处理通过专用充电器进行的充电，需要：
<ul>
<li>将 UfxChipidea 或 Ufxsynopsys 作为客户端驱动程序加载到 UFX。</li>
<li>在 WDK 中包括 Ufxproprietarycharger。</li>
</ul></td>
<td><p><strong>UFX 的体系结构</strong></p>
<p>熟悉 Microsoft 提供的 USB 驱动程序堆栈：</p>
<a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">Windows 中的 USB 设备端驱动程序</a>
<p><strong>熟悉 UFX 对象和句柄</strong></p>
<p>UFX 扩展了 WDF 对象功能，以定义其自己的特定于 USB 的 UCX 对象。 有关 WDF 对象的更多详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects" data-raw-source="[Introduction to Framework Objects](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)">框架对象简介</a>。</p>
<p>对于排队请求，UFX 使用特定于 USB 的对象。 有关详细信息，请<a href="ufx-objects-and-handles-used-by-a-usb-function-controller.md" data-raw-source="[UFX objects and handles used by a USB function client driver](ufx-objects-and-handles-used-by-a-usb-function-controller.md)">UFX USB 函数客户端驱动程序使用的对象和句柄</a>。</p>
<p><strong>编写函数控制器客户端驱动程序</strong></p>
<p>了解 UFX 的行为，该行为与客户端驱动程序交互的方式以及客户端驱动程序应实现的功能。</p>
<p><a href="function-client-driver.md" data-raw-source="[Tasks for a function controller client driver](function-client-driver.md)">函数控制器客户端驱动程序的任务</a></p>
<p><strong>编程参考节</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#function-class-driver-reference" data-raw-source="[USB function class driver to UFX programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#function-class-driver-reference)">UFX 编程参考的 USB 函数类驱动程序</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usb-function-controller-client-driver-reference" data-raw-source="[USB function controller client driver programming reference](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usb-function-controller-client-driver-reference)">USB 函数控制器客户端驱动程序编程参考</a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#filter-driver-for-supporting-usb-chargers" data-raw-source="[USB filter driver for supporting proprietary chargers](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#filter-driver-for-supporting-usb-chargers)">用于支持专用充电器的 USB 筛选器驱动程序</a></p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[通用串行总线 (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



