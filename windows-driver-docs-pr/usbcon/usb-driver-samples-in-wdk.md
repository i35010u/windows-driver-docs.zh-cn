---
Description: 本主题包含了可从 GitHub 上的 Windows 驱动程序示例存储库下载的 USB 示例有关的基本信息。
title: USB 驱动程序示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e8cecce9ec3e6ae3488f999674fdfb1095f664a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356602"
---
# <a name="usb-driver-samples"></a>USB 驱动程序示例


本主题包含了可从下载的 USB 示例有关的基本信息[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

## <a name="usb-samples"></a>USB 示例


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>示例名称</th>
<th>示例说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618936" data-raw-source="[WDF Sample Driver Learning Lab for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618936)">WDF 示例驱动程序的 OSR USB FX2 学习实验室</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618002" data-raw-source="[Sample UMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618002)">OSR USB FX2 示例 UMDF 函数驱动程序</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618937" data-raw-source="[Sample KMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618937)">OSR USB FX2 示例 KMDF 函数驱动程序</a></p></td>
<td><p>OSRUSBFX2 示例演示如何执行大容量并使用 Microsoft Windows 驱动程序框架 (WDF) 中断数据传输到通用串行总线 (USB) 设备。 此示例是面向 OSR USB FX2 学习工具包。 设备的规范，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=64091" data-raw-source="[Using the OSR USB FX-2 Learning Kit V2.0](https://go.microsoft.com/fwlink/p/?linkid=64091)">使用 OSR USB FX 2 学习工具包 V2.0</a>。</p></td>
</tr>
<tr class="even">
<td><a href="https://go.microsoft.com/fwlink/p/?LinkId=618938" data-raw-source="[USBSAMP](https://go.microsoft.com/fwlink/p/?LinkId=618938)">USBSAMP</a></td>
<td><p>USBSAMP 示例演示如何使用 Windows 驱动程序框架 (WDF) 执行大容量和同步数据传输到通用的 USB 设备。 对于 Intel 82930 USB 测试板编写这个示例。 它包含控制台测试应用程序，以启动大容量和同步传输并获取有关设备的 I/O 终结点信息。 该应用程序还演示如何使用基于 GUID 的设备名称和生成操作系统使用的管道名称<strong>SetupDiXXX</strong>用户模式 Api。</p></td>
</tr>
<tr class="odd">
<td><a href="https://go.microsoft.com/fwlink/p/?LinkId=618004" data-raw-source="[USBVIEW](https://go.microsoft.com/fwlink/p/?LinkId=618004)">USBVIEW</a></td>
<td><p>USBVIEW 示例演示如何在用户模式应用程序可以枚举 USB 主控制器、 USB 集线器和附加的 USB 设备，并可以查询有关注册表中和通过 USB 请求到的设备的设备的信息。 USBVIEW 基于 Windows 驱动程序模型 (WDM) 上。</p>
<div class="alert">
<strong>请注意</strong>USBView 工具，获取可执行文件从 Windows Driver Kit (WDK) (工具&lt;em&gt;&lt;arch&gt; </em>文件夹)。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="building-a-sample"></a>生成示例


有关生成的示例驱动程序的信息，请参阅[开发、 测试和部署驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。

## <a name="related-topics"></a>相关主题
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)  



