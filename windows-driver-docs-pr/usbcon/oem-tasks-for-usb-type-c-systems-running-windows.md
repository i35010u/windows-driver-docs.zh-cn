---
Description: 此表描述了使用情况下支持的 Windows 10 中，并为这些用例工作，必须执行其他任务 Oem。
title: USB 类型 C 系统的 OEM 任务
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c82a8d7a88289e19d547fa006ea07accabd08ee7
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463896"
---
# <a name="oem-tasks-for-usb-type-c-systems"></a>USB 类型 C 系统的 OEM 任务


\[有些信息与预发布产品的商业发布之前可能有大幅度修改。 Microsoft 不做任何明示或暗示的担保，此处提供的信息。\]

此表描述了使用情况下支持的 Windows 10 中，并为这些用例工作，必须执行其他任务 Oem。




<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>用例</th>
<th>Windows 支持</th>
<th>OEM 任务</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Power 交付</strong></p>
<p>对使用旧的充电器充电 USB C 类型系统的支持 (&lt;7.5W)，USB 类型 C 充电器 (&lt;15W)，Power 交付充电器 （100W +）</p></td>
<td><p>对于 Windows 10 移动版的系统，</p>
<ul>
<li>由从旧的充电器充电<a href="usb-device-side-drivers-in-windows.md" data-raw-source="[USB device-side drivers in Windows](usb-device-side-drivers-in-windows.md)">USB 设备端驱动程序在 Windows 中的</a>。</li>
<li>USB 连接器管理器驱动程序处理从 USB C 类型 （包括那些实现 Power 交付） 充电器，收费：USB 连接器管理器类扩展 (UcmCx) 和连接器及其客户端驱动程序。 客户端驱动程序与硬件来确定计费策略进行通信，并将转发该 UcmCx，进一步将其发送到充电仲裁驱动程序 (CAD)。 CAD 选择要使用的计费源。</li>
</ul>
<p>适用于 Windows 10 桌面版 （主页、 专业版、 企业版和教育） 系统，</p>
<ul>
<li>不建议从旧的充电器充电，因为它们不是功能强大，足以桌面系统进行收费。</li>
<li>为 USB 类型 C 充电器充电由 USB 连接器管理器类扩展 (UcmCx) 和连接器及其客户端驱动程序处理。 系统当前未指定要使用的电源和消耗多少能源。</li>
</ul>
<p></p>
<div class="alert">
<strong>请注意</strong>  检测到较慢的充电器时通知用户。
</div>
<div>
 
</div></td>
<td><p>您必须确定硬件、 固件和客户端驱动程序中的计费策略。 主要充电策略包括：</p>
<ul>
<li>电源 （提供程序） 或 power 接收器 （使用者） 是系统？</li>
<li>系统应消耗多少能源？</li>
<li>如果有多个 power 源 （如充电器） 可用，则应使用哪些电源 （充电器）？</li>
</ul>
<p>有关 power 符合交付的充电器，硬件必须协商 power 协定，其中包括电压和 current。 协商的 power 协定必须转发到通过 USB 连接器管理器类扩展 (UcmCx) 或相应的措施的 USCI 驱动程序的系统。</p>
<p>如果慢速充电器连接到系统，必须通过 UcmCx 或 UCSI 通知系统。</p>
<p>若要支持旧的专有高电压或高当前收费机制，附加的筛选器驱动程序必须针对编写 Microsoft 的现成 USB 函数驱动程序检测到专有充电器并报告给现成驱动程序。</p>
<p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">编写 USB 类型 C 连接器驱动程序</a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt188012" data-raw-source="[USB filter driver for supporting proprietary chargers](https://msdn.microsoft.com/library/windows/hardware/mt188012)">支持专有充电器 USB 筛选器驱动程序</a></p>
<div class="alert">
<strong>请注意</strong>  Windows 不支持 Power 传递旧的 USB A 和 USB B USB microB 连接器。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td><p><strong>连接 USB 设备和外围设备</strong></p>
<p>连接 USB 设备/外围设备 （桌面和移动版） 的 Windows 系统的功能</p></td>
<td><p>Windows 10 的桌面版本中支持大多数设备类。 在 Windows 中包含的设备驱动程序和其安装文件</p>
<p>运行 Windows 10 移动版的设备可以连接并与 USB 设备/外围设备通过一系列现成的驱动程序进行交互。 操作系统支持的设备类的一个子集。</p>
<p>查看，请<a href="supported-usb-classes.md" data-raw-source="[USB device class drivers included in Windows](supported-usb-classes.md)">USB 设备类驱动程序包含在 Windows 中</a>。</p></td>
<td><p>如果您的系统想要连接到自定义的 USB 设备，Windows 不包括驱动程序，可以选择要加载的通用驱动程序 (Winusb.sys) 或编写驱动程序。 有关指南，请参阅<a href="winusb-considerations.md" data-raw-source="[Choosing a driver model for developing a USB client driver](winusb-considerations.md)">选择用于开发 USB 客户端驱动程序的驱动程序模型</a>。</p>
<p>我们建议您编写单个驱动程序在 Windows 10 上运行的桌面版和 Windows 10 移动版。 有关详细信息，请参阅<a href="https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers" data-raw-source="[Getting Started with Universal Windows drivers](https://msdn.microsoft.com/windows-drivers/develop/getting_started_with_universal_drivers)">通用 Windows 驱动程序入门</a>。</p>
<p>若要编写通信设备的应用程序，使用 Windows 运行时 Api。 有关详细信息，请参阅<a href="talking-to-usb-devices-start-to-finish.md" data-raw-source="[Talking to USB devices, start to finish (UWP app)](talking-to-usb-devices-start-to-finish.md)">与 USB 设备通信，启动以完成 （UWP 应用）</a>。</p></td>
</tr>
<tr class="odd">
<td><strong>备用模式</strong>
<p>连接到非 USB 设备 （例如监视） 使用 USB 类型 C 连接器。</p>
 </td>
<td><p>Windows 10 是能够检测 DisplayPort/DockPort 设备，如果硬件支持这些其他模式。</p>
<p>Windows 10 的宣传位置设备提供现成驱动程序，并通知用户，如果布告栏设备将指示发生了错误。</p></td>
<td><p>为了使备用模式工作，您的系统和设备必须支持硬件和固件的备用模式。 执行必需任务来协商的备用模式和输入模式。 它是通常来实现的 muxing 通过网络传输到备用模式 USB 类型 C 连接器上的。</p></td>
</tr>
<tr class="even">
<td><strong>宣传位置设备</strong>
<p>显示有关错误条件，以帮助用户解决问题的信息。</p></td>
<td><p>Windows 10 的宣传位置设备提供现成驱动程序，并通知用户，如果布告栏设备将指示错误。</p>
<p>用户可能会看到错误通知：</p>
<ul>
<li>备用模式不支持通过 PC 或运行 Windows 10 的电话。</li>
<li>备用模式不支持的电缆 （如果使用）。</li>
</ul>
为获得最佳结果，请确保通过 PC 或电话或电缆满足备用模式设备或适配器的要求。
<p></p></td>
<td><p>备用模式适配器或设备必须实现布告栏设备，该值指示备用模式协商成功。</p>
<p>如果你的备用模式适配器或设备实现了 USB 的其他功能，在更新的宣传位置描述符内容时将需要你断开并重新连接该设备，可能会中断功能 (如文件传输，如果你的设备是一个 USB 大容量存储设备）。 若要避免这种情况，布告栏规范建议在你的设备，使用的集成的中心，并且具有布告栏设备显示为一个单独的 USB 设备上其端口之一。</p>
<p>有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=620207" data-raw-source="[USB Device Class Definition for Billboard Devices specification](https://go.microsoft.com/fwlink/p/?linkid=620207)">布告栏设备规范的 USB 设备类定义</a>。</p></td>
</tr>
<tr class="odd">
<td><strong>USB 双角色</strong>
<p>将两个 Windows 设备连接在一起</p></td>
<td><p>当两个 Windows 设备连接在一起时，系统将确定相应的角色的每个设备应位于和执行角色交换操作，必要时。</p>
<p>若要支持此功能，Windows 10 可以与通过 USB 角色切换类扩展框架的系统上的双角色控制器通信。 Synopsys 双角色控制器还提供了此框架的收件箱客户端驱动程序。</p>
<p>对于 USB C 类型系统，USB 连接器管理器获取硬件端口控制器最初分配的角色有关的信息。</p>
<p>USB 角色切换堆栈和 USB 连接器管理器堆栈与硬件来获取当前角色，并根据需要交换系统的端口的角色通信。</p>
<p></p>
<div class="alert">
<strong>请注意</strong>  C 类型的对等 USB 如 PC 连接到另一台 PC 或移动设备连接到另一台移动设备不支持连接。 对于此类连接，向用户显示错误。
</div>
<div>
 
</div></td>
<td><p>双角色端口必须与操作系统以确保在正确的时间加载适当的软件堆栈 （主机或函数） 合作。</p>
<p>可以设计系统，以便双角色 USB 端口需要 Windows 配置为主机或函数的模式。 这些设计将需要使用 USB 角色切换堆栈。 如果系统不使用 Synopsys 或 ChipIdea 双角色控制器，你需要为系统的双角色控制器编写 USB 角色切换客户端驱动程序。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt628026" data-raw-source="[USB dual-role controller driver programming reference](https://msdn.microsoft.com/library/windows/hardware/mt628026)">USB dual-role controller driver programming reference</a>（USB 双角色控制器驱动程序编程参考）</p>
<p>系统还可以设计，以便在固件或客户提供的驱动程序为主机或函数的端口，具体取决于连接到端口的设备配置的端口。 这些设计将需要为实现此逻辑在固件中或将需要在 USB 连接器管理器客户端驱动程序中实现它。 在这些系统中，Windows 将自动加载正确的软件堆栈。</p>
<p><a href="bring-up-a-usb-type-c-connector-on-a-windows-system.md" data-raw-source="[Write a USB Type-C connector driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)">编写 USB 类型 C 连接器驱动程序</a></p></td>
</tr>
<tr class="even">
<td><strong>音频附件</strong>
<p>USB C 型连接器可以用作的音频插孔。</p></td>
<td>如果硬件支持的功能，Windows 10 是作为 3.5mm 音频插孔，检测 USB 类型 C 模拟输入的支持。
<p>USB 类型 C 规范连接器允许 USB 类型 C 连接器，以使用通过使用音频附件模式类似于一个 3.5 英寸模拟音频插孔。 Windows 10 支持通过检测为正则 3.5"模拟音频设备附件实现音频 accessories USB C 类型支持的系统。</p></td>
<td>若要使用此功能，你的硬件或固件必须检测如果音频附件已连接并切换到该模式下，根据音频类型 C 规范。 这是通过将 3.5 英寸模拟音频连接器上的针映射到 USB 类型 C 连接器上的 pin。</td>
</tr>
</tbody>
</table>

 

USB 类型 C 连接器可以使用有线停靠，它允许系统以连接到传递到系统的电源，并将附加其他外围设备的停靠。 如果系统检测到的备用显示，系统可以投影到该显示。 若要启用有线停靠，请确保已完成 Power 交付、 连接 USB 设备和外围设备，为列出的 OEM 任务和其他模式上表中的用例。

## <a name="related-topics"></a>相关主题
[Windows 支持 USB 类型 C 连接器](oem-tasks-for-bringing-up-a-usb-typec.md)  



