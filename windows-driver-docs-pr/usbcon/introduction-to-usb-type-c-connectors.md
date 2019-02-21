---
Description: Possible causes and resolutions to troubleshooting messages in Windows 10 that users might get on USB Type-C systems running Windows.
title: 对 USB 类型 C Windows 系统的消息进行故障排除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2581654f6d6c5c11d6f7dcac2657d9dfab08b3d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525981"
---
# <a name="troubleshoot-messages-for-a-usb-type-c-windows-system"></a>对 USB 类型 C Windows 系统的消息进行故障排除


可能的原因以及故障排除的用户可能会在运行 Windows 的 USB 类型 C 系统的 Windows 10 中的消息的解决方法。

对称和可逆设计的 USB 类型 C 连接器允许用户连接运行 Windows 连接任何 USB 类型 C 设备，并使用新功能，例如增强的收费和其他模式的系统。 但是，硬件和/或软件限制某些组合可能会阻止其中某些功能工作正常。 Windows 10 提供了一套 USB 类型 C 通知，以帮助用户解决这些问题。

在本主题中，USB 类型 C 系统是指运行 Windows 10 桌面版 （主页、 专业版、 企业版和教育版） 或运行 Windows 10 移动版的移动设备的电脑。

**与系统的 USB 类型 C 连接器相关的故障排除消息**

-   [您可能能够解决您的 USB 设备](#-1)
-   [设备正在充电缓慢](#-2)
-   [USB 设备可能无法工作](#-3)
-   [请尝试改进 USB 连接](#-4)
-   [显示连接被限制](#-5)
-   [这些两台 Pc （移动设备） 不能进行通信](#-6)

## <a href="" id="-1"></a>您可能能够解决您的 USB 设备


* * USB 设备遇到了问题。 请按照下列步骤以尝试修复此错误。 (错误代码\_ \_ \_ \_) * *

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>建议的解决方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>设备硬件报告了一个问题或设备驱动程序出现了故障。</p></td>
<td><ol>
<li>请注意错误代码。
<ul>
<li>在 Windows 10 桌面版系统中，打开设备管理器，并查找设备。 它&#39;s 标有一个黄色感叹号。 右键单击节点并打开设备属性。 错误代码是下<strong>设备状态</strong>。</li>
<li>在 Windows 10 移动版系统中，通知会显示错误代码。</li>
</ul></li>
<li>请按照中所述的故障排除步骤<a href="https://go.microsoft.com/fwlink/p/?LinkId=526896" data-raw-source="[this article](https://go.microsoft.com/fwlink/p/?LinkId=526896)">这篇文章</a>。</li>
</ol>
<div class="alert">
<strong>请注意</strong>适用于在设备管理器中除代码 28 所示的所有错误代码。
</div>
<div>

</div></td>
</tr>
</tbody>
</table>



## <a href="" id="-2"></a>设备正在充电缓慢


**若要加快收费，使用的充电器和随设备附带的电缆。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>建议的解决方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>充电器不兼容与你的系统。
<div class="alert">
<strong>请注意</strong>非 USB 类型 C 充电器支持 USB 电池充电 1.2 规范。 这些充电器的一些使用专有充电的机制。 您的系统可能不支持所有这些充电器。
</div>
<div>

</div></li>
<li>充电器不是功能强大，足以收费系统。</li>
<li>充电器未连接到计费系统的端口。</li>
<li>充电电缆不符合充电器或系统电源的要求。</li>
</ul>
<div class="alert">
<strong>注意</strong><br/><p>使用 USB 类型 C 连接器的系统具有更高版本的 power 限制，它可以支持多达 5V、 3A，15W。 如果连接器就支持<a href="https://go.microsoft.com/fwlink/p/?LinkID=623310" data-raw-source="[USB Power Delivery](https://go.microsoft.com/fwlink/p/?LinkID=623310)">USB 供电</a>（行业标准），它可以更快地收取费用更高的电源级别。</p>
<p>为了使您可以获得快速充电权益，您的系统、 充电器和电缆必须支持行业标准。 此外，你的充电器和电缆必须支持系统以最佳方式对其计费所需的电源级别。 例如，如果您的系统要求 12V 和 3A 进行收费，5V 3A 充电器不能以最佳方式收费系统。</p>
</div>
<div>

</div></td>
<td><ul>
<li>使用充电器和随设备附带的电缆。</li>
<li>请确保你&#39;重新连接到你的系统上充电 USB 类型 C 端口在充电器。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-3"></a>USB 设备可能无法工作


**请尝试连接到 PC。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>建议的解决方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>已连接设备的驱动程序不支持的系统上运行的 Windows 版本上。 有关受支持的设备的信息，请参阅<a href="supported-usb-classes.md" data-raw-source="[USB device class drivers included in Windows](supported-usb-classes.md)">USB 设备类驱动程序包含在 Windows 中</a>。</p>
<div class="alert">
<strong>请注意</strong>移动系统能够与其他 USB 外围设备连接。 但是，并非所有连接到 PC 的设备可以连接到移动系统。 检查受支持的设备到前面的列表。
</div>
<div>

</div></td>
<td><ul>
<li>请确保正在运行 Windows 的最新版本，以便您具有最新驱动程序包。 有关信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkID=698739" data-raw-source="[Windows 10 Updates](https://go.microsoft.com/fwlink/p/?LinkID=698739 )">Windows 10 更新</a>。</li>
<li>如果你已在运行最新版本，请尝试改为连接到 PC 的设备。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-4"></a>请尝试改进 USB 连接


**请确保要连接到该设备支持和使用的正确的电缆。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>建议的解决方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>设备连接使用 new USB 类型 C 功能不受您的系统。</li>
<li>已使用新的 USB 类型 C 功能不支持的电缆连接设备。</li>
</ul>
<p>USB 类型 C 引入了新功能称为备用模式，从而允许非 USB 协议可以在 USB 类型 C 电缆上运行。 例如，使用备用模式的停靠有能力通过 USB 传输视频信号。</p>
<p>为了使备用模式工作，硬件和 PC/电话的设备或适配器上的软件必须支持备用模式。 此外，某些其他模式可能需要特定的 USB 类型 C 电缆。</p></td>
<td><ul>
<li>请确保您的系统支持连接的设备的功能。</li>
<li>请确保将电缆连接支持连接的设备的功能。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-5"></a>显示连接被限制


**DisplayPort/MHL 连接可能无法工作。请尝试使用另一条电缆。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>建议的解决方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>系统不支持这些新 USB 类型 C 功能已连接设备。</li>
<li>已使用新的 USB 类型 C 功能不支持的电缆连接设备。</li>
</ul>
<p>USB 类型 C 引入了名为其他模式的新功能。 该功能允许非 USB 协议通过 USB 类型 C 电缆，运行时同时保留 USB 2.0 和计费功能。 下面是显示备用模式：</p>
<ul>
<li><p><strong>DisplayPort</strong> /<strong>DockPort</strong></p>
<p>此备用模式允许用户通过 USB 连接器投影到外部 DisplayPort 显示音频/视频。</p></li>
<li><p><strong>MHL</strong></p>
<p>MHL 备用模式是允许对项目视频/音频向外部用户显示支持 MHL。</p></li>
</ul>
<p>硬件和软件系统、 设备或适配器或电缆上的不支持<strong>DisplayPort</strong> /<strong>DockPort</strong>或<strong>MHL</strong>备用模式。</p></td>
<td><ul>
<li>请确保系统、 设备和电缆支持<strong>DisplayPort</strong> /<strong>DockPort</strong>或<strong>MHL</strong>备用模式。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-6"></a>这些两台 Pc （移动设备） 不能进行通信


**尝试连接到移动设备 (PC)，以实现你的目标其中之一。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>建议的解决方案</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>无法连接两台运行 Windows 10 桌面版的 Pc。</li>
<li>无法连接两个运行 Windows 10 移动版的移动设备。</li>
</ul></td>
<td>不支持此连接方案。</td>
</tr>
</tbody>
</table>










