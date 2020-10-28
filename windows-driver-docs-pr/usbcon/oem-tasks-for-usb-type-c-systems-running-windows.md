---
description: 此表描述了 Windows 10 支持的用例，而 Oem 必须执行其他任务才能使用这些用例。
title: USB 类型 C 系统的 OEM 任务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7170bb5be458664f0ce3ebb33af4c03c4e1c6814
ms.sourcegitcommit: be37c8ccfe838869eec6fae4112017eb6a96d848
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92630152"
---
# <a name="oem-tasks-for-usb-type-c-systems"></a>USB 类型 C 系统的 OEM 任务


\[某些信息与预发布的产品相关，这些信息可能会在正式发布之前进行重大修改。 Microsoft 对此处提供的信息不提供任何明示或暗示的保证。\]

此表描述了 Windows 10 支持的用例，而 Oem 必须执行其他任务才能使用这些用例。




<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>使用案例</th>
<th>Windows 支持</th>
<th>OEM 任务</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>电源交付</strong></p>
<p>支持使用旧的充电器 (&lt; 7.5 w) 、Usb 类型 c 充电器 (&lt; 15W) 、电源交付充电器 (100W +) 对 USB 类型 c 系统进行收费</p></td>
<td><p>对于 Windows 10 移动版系统，</p>
<ul>
<li>从旧式充电器中收取的费用由 <a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">Windows 中的 USB 设备端驱动程序</a>处理。</li>
<li>从 USB 类型 C 充电器（包括那些实现电源传递) 的 (）中收取的费用由 USB 连接器管理器驱动程序处理： USB 连接器管理器类扩展 (UcmCx) 及其客户端驱动程序的连接器。 客户端驱动程序与硬件通信，以确定充电策略并转发该 UcmCx，这会进一步将其发送到收费仲裁驱动程序 (CAD) 。 CAD 选择要使用的收费来源。</li>
</ul>
<p>对于桌面版 (适用于 Windows 10 的 Windows 10 家庭版、专业版、企业版和教育版) 系统。</p>
<ul>
<li>不建议从旧的充电器收费，因为它们的功能不足以对桌面系统计费。</li>
<li>USB 类型 C 充电器的充电由 USB 连接器管理器类扩展 (UcmCx) 及其客户端驱动程序处理。 系统当前未指定要使用的电源和使用的电量。</li>
</ul>
<p></p>
<div class="alert">
<strong>注意</strong>  检测到慢速充电器时，会通知用户。
</div>
<div>
 
</div></td>
<td><p>你必须确定硬件、固件和客户端驱动程序中的充电策略。 收费政策主要包括：</p>
<ul>
<li>系统 (提供商) 还是 power sink (使用者) ？</li>
<li>系统应该消耗多少能源？</li>
<li>如果有多个 power source (如充电器) ，应使用哪些电源 (充电器) ？</li>
</ul>
<p>对于符合电源交付标准的充电器，硬件必须协商电源合同，其中包括电压和电流。 必须通过 USB 连接器管理器类扩展 (UcmCx) 或 USCI 驱动程序以进行适当的操作，将协商的电源协定转发到系统。</p>
<p>如果慢速充电器连接到系统，则必须通过 UcmCx 或 UCSI 通知系统。</p>
<p>若要支持传统的高电压或高电流充电机制，必须为 Microsoft 的内置 USB 函数驱动程序编写一个新的筛选器驱动程序，该驱动程序检测专有充电器并将其报告给内置驱动程序。</p>
<p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">编写 USB 类型 C 连接器驱动程序</a></p>
<p><a href="/previous-versions/windows/hardware/drivers/mt188012(v=vs.85)" data-raw-source="[USB filter driver for supporting proprietary chargers](/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))">用于支持专用充电器的 USB 筛选器驱动程序</a></p>
<div class="alert">
<strong>注意</strong>  Windows 不支持旧式 USB-A 和 USB-B/microB 连接器的电源交付。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p><strong>连接 USB 设备和外围设备</strong></p>
<p>Windows 系统 (桌面和移动) 连接 USB 设备/外设的能力</p></td>
<td><p>适用于桌面版的 Windows 10 支持大多数的设备类。 设备驱动程序及其安装文件包含在 Windows 中</p>
<p>运行 Windows 10 移动版的设备可以通过一组内置驱动程序连接 USB 设备/外围设备并与之交互。 操作系统支持设备类的一个子集。</p>
<p>请参阅 <a href="supported-usb-classes.md" data-raw-source="[USB device class drivers included in Windows](supported-usb-classes.md)">Windows 附带的 USB 设备类驱动程序</a>。</p></td>
<td><p>如果你的系统要连接到 Windows 不包含驱动程序的自定义 USB 设备，你可以选择加载通用驱动程序 ( # A0) 或编写驱动程序。 有关指南，请参阅 <a href="winusb-considerations.md" data-raw-source="[Choosing a driver model for developing a USB client driver](winusb-considerations.md)">选择用于开发 USB 客户端驱动程序的驱动程序模型</a>。</p>
<p>建议编写一个在 Windows 10 上运行的用于桌面版和 Windows 10 移动版的驱动程序。 有关详细信息，请参阅<a href="/windows-hardware/drivers" data-raw-source="[Getting Started with Universal Windows drivers](/windows-hardware/drivers)">通用 Windows 驱动程序入门</a>。</p>
<p>若要编写与设备通信的应用程序，请使用 Windows 运行时 Api。 有关详细信息，请参阅 <a href="talking-to-usb-devices-start-to-finish.md" data-raw-source="[Talking to USB devices, start to finish (UWP app)](talking-to-usb-devices-start-to-finish.md)">与 USB 设备对话、开始 (UWP 应用) </a>。</p></td>
</tr>
<tr class="odd">
<td><strong>备用模式</strong>
<p>使用 USB C # C # 连接到非 USB 设备 (例如，监视) 。</p>
 </td>
<td><p>如果硬件支持这些备用模式，Windows 10 能够检测 DisplayPort/DockPort 设备。</p>
<p>Windows 10 为布告栏设备提供内置驱动程序，如果布告栏设备指示出现错误，则会通知用户。</p></td>
<td><p>为了使备用模式正常工作，系统和设备必须支持硬件和固件中的备用模式。 执行必要的任务以协商备用模式并进入模式。 通常通过将 USB C # 连接器上的 muxing 到备用模式来完成此操作。</p></td>
</tr>
<tr class="even">
<td><strong>布告栏设备</strong>
<p>显示有关错误条件的信息，以帮助用户解决问题。</p></td>
<td><p>Windows 10 提供适用于布告栏设备的内置驱动程序，如果布告栏设备指示出现错误，则通知用户。</p>
<p>如果出现以下情况，则用户可能会看到错误通知：</p>
<ul>
<li>运行 Windows 10 的电脑或手机不支持备用模式。</li>
<li>如果) 使用，则电缆 (不支持备用模式。</li>
</ul>
为获得最佳结果，请确保电脑或电话或电缆满足备用模式设备或适配器的要求。
<p></p></td>
<td><p>备用模式适配器或设备必须实现一个布告栏设备，指示备用模式协商是否成功。</p>
<p>如果备用模式适配器或设备实现其他 USB 功能，则更新布告栏描述符的内容将要求您断开和重新连接该设备，可能会中断功能 (例如文件传输）（如果您的设备是 USB 大容量存储设备) 。 为避免出现这种情况，布告栏规范建议使用设备中的集成集线器，并使布告栏设备在其某个端口上显示为单独的 USB 设备。</p>
<p>有关详细信息，请参阅 <a href="https://www.usb.org/document-library/billboard-device-class-spec-revision-121-and-adopters-agreement" data-raw-source="[USB Device Class Definition for Billboard Devices specification](https://www.usb.org/document-library/billboard-device-class-spec-revision-121-and-adopters-agreement)">布告栏设备的 USB 设备类定义规范</a>。</p></td>
</tr>
<tr class="odd">
<td><strong>USB 双重角色</strong>
<p>将两个 Windows 设备连接在一起</p></td>
<td><p>当两个 Windows 设备连接在一起时，系统将确定每个设备应处于的适当角色并在需要时执行角色交换操作。</p>
<p>为支持这种情况，Windows 10 可以通过 USB 角色交换机类扩展框架与系统上的双重角色控制器进行通信。 还为 Synopsys 双重角色控制器提供了此框架的收件箱客户端驱动程序。</p>
<p>对于 USB 类型 C 系统，USB 连接器管理器将获取有关硬件端口控制器最初分配的角色的信息。</p>
<p>USB 角色切换堆栈和 USB 连接器管理器堆栈与硬件通信以获取当前角色，并根据需要交换系统端口的角色。</p>
<p></p>
<div class="alert">
<strong>注意</strong>  对等 USB 类型-C 连接（如电脑）连接到另一台电脑，或者移动设备连接到其他移动设备。 对于此类连接，向用户显示错误。
</div>
<div>
 
</div></td>
<td><p>双角色端口必须与操作系统结合使用，以确保正确的软件堆栈 (在正确的时间加载主机或函数) 。</p>
<p>系统可设计为双重角色 USB 端口需要 Windows 将其配置为主机或函数模式。 这些设计需要使用 USB 角色切换堆栈。 如果系统不使用 Synopsys 或 ChipIdea 双重角色控制器，则需要为系统的双角色控制器写入 USB 角色切换客户端驱动程序。</p>
<p><a href="/previous-versions/windows/hardware/drivers/mt628026(v=vs.85)" data-raw-source="[USB dual-role controller driver programming reference](/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))">USB 双角色控制器驱动程序编程参考</a></p>
<p>系统还可以设计为使固件或客户提供的驱动程序将该端口配置为主机或函数端口，具体取决于连接到该端口的设备。 这些设计需要在固件中实施这种逻辑，或者需要在 USB 连接器管理器客户端驱动程序中实现它。 在这些系统中，Windows 将自动加载正确的软件堆栈。</p>
<p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">编写 USB 类型 C 连接器驱动程序</a></p></td>
</tr>
<tr class="even">
<td><strong>音频附件</strong>
<p>USB 类型 C 连接器可以用作音频插孔。</p></td>
<td>如果硬件支持此功能，Windows 10 可检测 USB 类型为 C 的模拟输入作为 3.5 mm 音频插孔。
<p>USB Type-C 规范连接器允许 USB 类型 C 连接器与 3.5 "模拟音频插孔" 一起使用（使用音频附件模式）。 Windows 10 通过检测附件作为常规的 3.5 "模拟音频设备，支持对音频附件实现 USB 类型 C 支持的系统。</p></td>
<td>若要使用此功能，你的硬件或固件必须根据音频类型 C 规范检测是否已连接音频附件并切换到该模式。 这是通过将 3.5 "模拟音频连接器" 上的针脚映射到 USB C # C 连接器上的引脚来完成的。</td>
</tr>
</tbody>
</table>

 

USB 类型 C 连接器可用于有线插接，这允许系统连接到坞向系统供电并附加其他外设。 如果系统检测到备用显示器，则系统可以投影到该显示器。 若要启用有线插接，请确保已为电源交付、连接 USB 设备和外围设备以及备用模式使用事例在上表中列出了已完成的 OEM 任务。

## <a name="related-topics"></a>相关主题
[Windows 对 USB 类型 C 连接器的支持](oem-tasks-for-bringing-up-a-usb-typec.md)