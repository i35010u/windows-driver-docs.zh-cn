---
description: 本主题包含有关可从 GitHub 上的 Windows 驱动程序示例存储库中下载的 USB 示例的基本信息。
title: USB 驱动程序示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f62094b6ba774c851b0acdd41bcb6b957c2f87b
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010053"
---
# <a name="usb-driver-samples"></a>USB 驱动程序示例


本主题包含有关可从 GitHub 上的 [Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507) 存储库中下载的 USB 示例的基本信息。

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
<td><p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618936" data-raw-source="[WDF Sample Driver Learning Lab for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618936)">适用于 OSR 的 WDF 示例驱动程序学习实验室-FX2</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618002" data-raw-source="[Sample UMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618002)">OSR USB-FX2 的示例 UMDF 函数驱动程序</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?LinkId=618937" data-raw-source="[Sample KMDF Function Driver for OSR USB-FX2](https://go.microsoft.com/fwlink/p/?LinkId=618937)">OSR USB-FX2 的示例 KMDF 函数驱动程序</a></p></td>
<td><p>OSRUSBFX2 示例演示如何通过使用 Microsoft Windows 驱动程序框架 (WDF) ，对通用串行总线 (USB) 设备执行批量和中断数据传输。 此示例是针对 OSR USB-FX2 学习工具包编写的。 设备的规格可以在 <a href="https://go.microsoft.com/fwlink/p/?linkid=64091" data-raw-source="[Using the OSR USB FX-2 Learning Kit V2.0](https://go.microsoft.com/fwlink/p/?linkid=64091)">使用 OSR USB FX 教育套件</a>v2.0 中找到。</p></td>
</tr>
<tr class="even">
<td><a href="https://go.microsoft.com/fwlink/p/?LinkId=618938" data-raw-source="[USBSAMP](https://go.microsoft.com/fwlink/p/?LinkId=618938)">USBSAMP</a></td>
<td><p>USBSAMP 示例演示如何通过使用 Windows 驱动程序框架 (WDF) ，将批量和同步数据传输传输到一般 USB 设备。 此示例是针对 Intel 82930 USB 测试板编写的。 它包含一个控制台测试应用程序，用于启动大容量传输和同步传输，并获取有关设备 i/o 终结点的信息。 该应用程序还演示了如何使用操作系统使用 <strong>SetupDiXXX</strong> 用户模式 api 生成的基于 GUID 的设备名称和管道名称。</p></td>
</tr>
<tr class="odd">
<td><a href="https://go.microsoft.com/fwlink/p/?LinkId=618004" data-raw-source="[USBVIEW](https://go.microsoft.com/fwlink/p/?LinkId=618004)">USBVIEW</a></td>
<td><p>USBVIEW 示例演示了用户模式应用程序如何枚举 USB 主机控制器、USB 集线器和连接的 USB 设备，并可从注册表和通过 USB 请求向设备查询有关设备的信息。 USBVIEW 基于 (WDM) Windows 驱动模型。</p>
<div class="alert">
<strong>注意</strong> 对于 USBView 工具，请从 Windows 驱动程序工具包 (WDK 获取可执行文件，)  (工具 &lt; 全身 " &gt; &lt; &gt; </em> 文件夹) 。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

## <a name="building-a-sample"></a>生成示例


有关生成示例驱动程序的信息，请参阅 [开发、测试和部署驱动程序](/windows-hardware/drivers)。

## <a name="related-topics"></a>相关主题
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)