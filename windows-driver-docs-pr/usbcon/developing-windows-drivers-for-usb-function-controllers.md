---
description: 为 USB 功能控制器开发 Windows 驱动程序的概述
title: 为 USB 功能控制器开发 Windows 驱动程序的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00baf1dea82054ddf5e6feb8cb8aaa3782ff0c12
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969370"
---
# <a name="overview-of-developing-windows-drivers-for-usb-function-controllers"></a>为 USB 功能控制器开发 Windows 驱动程序的概述


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>目的</strong></p>
<p>本部分介绍 Windows 操作系统中的支持，用于开发通用串行总线 (USB) 函数控制器驱动程序，该驱动程序与 Microsoft 提供的 USB 函数控制器扩展 (UFX) 通信。</p>
<p><strong>开发工具和 Microsoft 提供的二进制文件</strong></p>
<p>Windows 驱动程序工具包 (WDK) 包含开发驱动程序所需的资源，如头文件、库、工具和示例。</p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=617155" data-raw-source="[Download kits and tools for Windows](https://go.microsoft.com/fwlink/p/?linkid=617155)">下载适用于 Windows 的工具包和工具</a></p>
<p>Windows 提供了收件箱 USB 函数控制器驱动程序，如 Synopsys IP 控制器硬件的 UfxSynopsys.sys。 它们通常需要平台级别的更改和验证，这些更改通常由硬件合作伙伴或 Oem 在启动平台时执行。 此启动过程可能包括与 ACPI 的集成，以通知系统驱动程序 USB 连接/分离事件，并使用 Microsoft 提供的 HLK 测试执行其他验证。 若要编写自己的控制器驱动程序，需要：</p>
<ul>
<li>UFX ( # A0) 加载为 FDO。 此驱动程序包含在 Windows 中。</li>
<li>链接到存根库 (Ufx01000) 。 该存根库在 WDK 中。 库转换由函数控制器驱动程序发出的调用，并将其传递给 UFX。</li>
<li>在 WDK 中包括 Ufxclient。</li>
</ul>
<p>若要从用户模式发送请求，需要：</p>
<ul>
<li>GenericUSBFn.sys 加载为 USB 函数类驱动程序。 此驱动程序包含在 Windows 中。</li>
<li>在 WDK 中包括 Genericusbfnioctl。</li>
</ul>
<p>若要从 USB 类驱动程序发送请求，需要：</p>
<ul>
<li>UFX ( # A0) 加载为 FDO。 此驱动程序包含在 Windows 中。</li>
<li>在 WDK 中包括 Usbfnioctl。</li>
</ul>
若要编写一个筛选器驱动程序来处理通过专用充电器进行的充电，需要：
<ul>
<li>UfxChipidea.sys 或 Ufxsynopsys.sys 作为客户端驱动程序加载到 UFX。</li>
<li>在 WDK 中包括 Ufxproprietarycharger。</li>
</ul></td>
<td><p><strong>UFX 的体系结构</strong></p>
<p>熟悉 Microsoft 提供的 USB 驱动程序堆栈：</p>
<a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">Windows 中的 USB 设备端驱动程序</a>
<p><strong>熟悉 UFX 对象和句柄</strong></p>
<p>UFX 扩展了 WDF 对象功能，以定义其自己的特定于 USB 的 UCX 对象。 有关 WDF 对象的更多详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects" data-raw-source="[Introduction to Framework Objects](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)">框架对象简介</a>。</p>
<p>对于排队请求，UFX 使用特定于 USB 的对象。 有关详细信息，请 <a href="ufx-objects-and-handles-used-by-a-usb-function-controller.md" data-raw-source="[UFX objects and handles used by a USB function client driver](ufx-objects-and-handles-used-by-a-usb-function-controller.md)">UFX USB 函数客户端驱动程序使用的对象和句柄</a>。</p>
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



