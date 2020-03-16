---
Description: Windows 10 中的消息疑难解答的可能原因和解决方法，用户可能会收到运行 Windows 的 USB 类型 C 系统。
title: USB 类型 C Windows 系统的消息疑难解答
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 060ecddcb41ae474d0845afc0b9f11216525c407
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242926"
---
# <a name="troubleshoot-messages-for-a-usb-type-c-windows-system"></a>USB 类型 C Windows 系统的消息疑难解答


Windows 10 中的消息疑难解答的可能原因和解决方法，用户可能会收到运行 Windows 的 USB 类型 C 系统。

USB C # C 连接器的对称和可逆设计允许用户将运行 Windows 的系统连接到连接任何 USB 类型 C 设备，并使用新功能，例如增强的充电和备用模式。 但是，某些硬件和/或软件限制组合可能会导致其中某些功能无法正常工作。 Windows 10 提供一组 USB 类型 C 通知，帮助用户解决这些问题。

在本主题中，USB 类型 C 系统指的是运行适用于桌面版的 Windows 10 （家庭版、专业版、企业版和教育版）或运行 Windows 10 移动版的移动设备的 PC。

**与系统的 USB 类型 C 连接器相关的疑难解答消息**

-   [可以修复 USB 设备](#-1)
-   [设备充电速度缓慢](#-2)
-   [USB 设备可能不工作](#-3)
-   [尝试改进 USB 连接](#-4)
-   [显示连接受到限制](#-5)
-   [这两台电脑（移动设备）无法通信](#-6)

## <a href="" id="-1"></a>可以修复 USB 设备


\* * USB 设备遇到问题。 请按照以下步骤尝试修复此问题。 （错误代码 \_\_\_\_） * *

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>推荐分辨率</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>设备硬件报告了问题或设备驱动程序出现故障。</p></td>
<td><ol>
<li>请注意错误代码。
<ul>
<li>在适用于桌面版的 Windows 10 系统上，打开设备管理器并找到设备。 它用黄色惊叹号标记。 右键单击该节点，然后打开 "设备属性"。 错误代码在 "<strong>设备状态</strong>" 下。</li>
<li>在 Windows 10 移动版系统上，通知将显示错误代码。</li>
</ul></li>
<li>请按照<a href="https://go.microsoft.com/fwlink/p/?LinkId=526896" data-raw-source="[this article](https://go.microsoft.com/fwlink/p/?LinkId=526896)">本文</a>中所述的故障排除步骤进行操作。</li>
</ol>
<div class="alert">
<strong>注意</strong> 适用于设备管理器中显示的所有错误代码，但代码28除外。
</div>
<div>

</div></td>
</tr>
</tbody>
</table>



## <a href="" id="-2"></a>设备充电速度缓慢


**若要加快充电速度，请使用设备附带的充电器和电缆。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>推荐分辨率</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>充电器与系统不兼容。
<div class="alert">
<strong>注意</strong> 非 USB 类型 C 充电器支持 USB 电池充电1.2 规范。 其中一些充电器使用专用的收费机制。 你的系统可能并不支持所有这些充电器。
</div>
<div>

</div></li>
<li>充电器的功能不足以对系统进行计费。</li>
<li>充电器未连接到系统的充电端口。</li>
<li>充电电缆不满足充电器或系统的电源要求。</li>
</ul>
<div class="alert">
<strong>注意</strong><br/><p>使用 USB 类型 C 连接器的系统具有更高的电源限制，最多可支持5V、3A、15W。 如果连接器支持<a href="https://go.microsoft.com/fwlink/p/?LinkID=623310" data-raw-source="[USB Power Delivery](https://go.microsoft.com/fwlink/p/?LinkID=623310)">USB 电源交付</a>（行业标准），则它可以更快地按更高的电源级别进行计费。</p>
<p>为了获得快速的充电权益，系统、充电器和电缆必须支持行业标准。 此外，你的充电器和电缆必须支持系统要求的电源级别，以便以最佳方式对其进行收费。 例如，如果您的系统需要使用12V 和3A 来充电，则5V，3A 充电器无法以最佳方式对您的系统充电。</p>
</div>
<div>

</div></td>
<td><ul>
<li>使用设备附带的充电器和电缆。</li>
<li>请确保将充电器连接到系统上的充电 USB 类型-C 端口。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-3"></a>USB 设备可能不工作


**尝试将其连接到 PC。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>推荐分辨率</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>系统上运行的 Windows 版本不支持所连接设备的驱动程序。 有关支持的设备的信息，请参阅<a href="supported-usb-classes.md" data-raw-source="[USB device class drivers included in Windows](supported-usb-classes.md)">Windows 附带的 USB 设备类驱动程序</a>。</p>
<div class="alert">
<strong>注意</strong> 移动系统能够与其他 USB 外围设备连接。 但是，并非所有连接到 PC 的设备都可以连接到移动系统。 将前面的列表检查到支持的设备。
</div>
<div>

</div></td>
<td><ul>
<li>请确保您运行的是最新版本的 Windows，以便您拥有最新的驱动程序包。 有关信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?LinkID=698739" data-raw-source="[Windows 10 Updates](https://go.microsoft.com/fwlink/p/?LinkID=698739 )">Windows 10 更新</a>。</li>
<li>如果已运行最新版本，请尝试将设备连接到 PC。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-4"></a>尝试改进 USB 连接


**请确保支持连接到的设备，并且使用正确的电缆。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>推荐分辨率</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>你已使用系统不支持的新 USB 类型 C 功能连接了设备。</li>
<li>已使用电缆不支持的新 USB 类型 C 功能连接了设备。</li>
</ul>
<p>USB 类型-C 引入了一个称为备用模式的新功能，它允许非 USB 协议通过 USB 类型 C 电缆运行。 例如，使用备用模式的停靠可以通过 USB 传输视频信号。</p>
<p>为了使备用模式正常工作，电脑/手机和设备或适配器上的硬件和软件必须支持备用模式。 此外，某些备用模式可能需要特定的 USB 类型-C 线。</p></td>
<td><ul>
<li>请确保系统支持连接的设备的功能。</li>
<li>请确保电缆支持连接的设备的功能。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-5"></a>显示连接受到限制


**DisplayPort/MHL 连接可能不起作用。尝试使用其他电缆。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>推荐分辨率</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>你已使用系统不支持的新 USB 类型 C 功能连接了设备。</li>
<li>已使用电缆不支持的新 USB 类型 C 功能连接了设备。</li>
</ul>
<p>USB 类型-C 引入了一项称为 "备用模式" 的新功能。 此功能允许非 USB 协议通过 USB 类型 C 电缆运行，同时保留 USB 2.0 和充电功能。 显示备用模式如下：</p>
<ul>
<li><p><strong>DisplayPort</strong> /<strong>DockPort</strong></p>
<p>此备用模式允许用户将音频/视频投影到外部 DisplayPort 通过 USB 连接器显示。</p></li>
<li><p><strong>MHL</strong></p>
<p>MHL 备用模式允许用户将视频/音频投影到支持 MHL 的外部显示器。</p></li>
</ul>
<p>系统上的硬件和软件、设备或适配器或电缆不支持<strong>DisplayPort</strong> /<strong>DockPort</strong>或<strong>MHL</strong>备用模式。</p></td>
<td><ul>
<li>请确保系统、设备和电缆支持<strong>DisplayPort</strong> /<strong>DockPort</strong>或<strong>MHL</strong>备用模式。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a href="" id="-6"></a>这两台电脑（移动设备）无法通信


**尝试将其中一个连接到移动设备（PC）以实现你的目标。**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>可能的原因</th>
<th>推荐分辨率</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>对于桌面版，不能连接两台运行 Windows 10 的电脑。</li>
<li>不能连接运行 Windows 10 移动版的两个移动设备。</li>
</ul></td>
<td>此连接方案不受支持。</td>
</tr>
</tbody>
</table>










