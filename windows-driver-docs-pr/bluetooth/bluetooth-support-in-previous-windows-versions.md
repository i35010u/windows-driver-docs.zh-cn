---
title: 以前的 Windows 版本中的蓝牙版本和配置文件支持
description: 以前的 Windows 版本中的蓝牙版本和配置文件支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a1ab044b254b6194dc7e98aed5a8fddde8f3a96
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798567"
---
# <a name="bluetooth-version-and-profile-support-in-previous-windows-versions"></a>以前的 Windows 版本中的蓝牙版本和配置文件支持


**注意**  
正在查找蓝牙音频设备的驱动程序？ 请参阅 [修复与蓝牙音频设备的连接和无线显示器](https://go.microsoft.com/fwlink/p/?LinkID=623629)。

 

**注意**  
有关 Windows 10 中的蓝牙支持的信息，请参阅 [windows 10 中的蓝牙支持](general-bluetooth-support-in-windows.md)。

 

## <a name="span-idwhich_previous_versions_of_windows_support_bluetooth_wireless_technology_spanspan-idwhich_previous_versions_of_windows_support_bluetooth_wireless_technology_spanspan-idwhich_previous_versions_of_windows_support_bluetooth_wireless_technology_spanwhich-previous-versions-of-windows-support-bluetooth-wireless-technology"></a><span id="Which_previous_versions_of_Windows_support_Bluetooth_wireless_technology_"></span><span id="which_previous_versions_of_windows_support_bluetooth_wireless_technology_"></span><span id="WHICH_PREVIOUS_VERSIONS_OF_WINDOWS_SUPPORT_BLUETOOTH_WIRELESS_TECHNOLOGY_"></span>哪些以前版本的 Windows 支持 Bluetooth 无线技术？


以下以前版本的 Windows 包含对蓝牙无线技术的内置支持：

所有 Sku 均 Windows 8.1 windows 8 的所有 sku windows 7 所有 windows 7 所有 sku windows XP Service Pack 2 (SP2) 和更高版本
-   注意： Windows XP Service Pack 1 (SP1) 版本支持的蓝牙无线技术，但使用的驱动程序仅适用于 PC 系统合作伙伴。 Windows XP Service Pack 2 (SP2) 将蓝牙无线技术支持集成到定期 Service Pack 版本中，并可供所有客户使用。

以下以前版本的 Windows **不** 支持蓝牙无线技术：

Windows server 2012 的所有 sku 所有 windows server 2008 R2 所有 sku windows server 2008 windows server 2003 all sku windows server windows server 的所有 sku windows 2000 虽然这些版本的 windows 没有内置的蓝牙无线技术支持，但在独立硬件供应商 (Ihv) ，可以使用第三方蓝牙驱动程序。

## <a name="span-idwhich_bluetooth_versions_do_previous_versions_of_windows_support_spanspan-idwhich_bluetooth_versions_do_previous_versions_of_windows_support_spanspan-idwhich_bluetooth_versions_do_previous_versions_of_windows_support_spanwhich-bluetooth-versions-do-previous-versions-of-windows-support"></a><span id="Which_Bluetooth_versions_do_previous_versions_of_Windows_support_"></span><span id="which_bluetooth_versions_do_previous_versions_of_windows_support_"></span><span id="WHICH_BLUETOOTH_VERSIONS_DO_PREVIOUS_VERSIONS_OF_WINDOWS_SUPPORT_"></span>以前版本的 Windows 支持哪些蓝牙版本？


Windows 支持蓝牙版本1.1 及更高版本。 请注意，蓝牙版本2.1 无线收发器和设备与早期版本的蓝牙向后兼容，将在不带 SP2 的 Windows XP 和 Windows Vista 上运行。 但是，这些 Windows 版本无法利用完整的蓝牙版本2.1 功能集，因为在发布 Windows Vista 之前，蓝牙版本2.1 规范未经过批准。

Windows 8 提供蓝牙智能准备，支持蓝牙版本4.0，并且能够与蓝牙智能设备连接。

Windows 对不同版本的蓝牙规范的支持取决于 Windows 版本，如下表所示：

<table>
<colgroup>
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
<col width="12%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">版本 1.1</th>
<th align="left">版本 2.0</th>
<th align="left">版本2.0，带有 EDR<em></th>
<th align="left">版本2。1</th>
<th align="left">版本2.1，带有 EDR</th>
<th align="left">4.0 版</th>
<th align="left">4.1 版</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>Windows 8.1</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows 8</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows 7</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista Service Pack 2 (SP2)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows Vista Service Pack 1 (SP1)</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p></em>*</p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
</tr>
<tr class="even">
<td align="left"><p>Windows Vista</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Windows XP</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
<td align="left"><p></p></td>
</tr>
</tbody>
</table>

 

\* 在 Windows Vista 和更高版本中启动的 EDR 支持相对于适用于 Windows XP 的蓝牙堆栈进行了增强。

\*\* 如果 Windows Vista SP1 包含仅供系统合作伙伴使用的包，则 Windows Vista SP1 支持蓝牙版本2.1。 Windows Vista SP2 将蓝牙版本2.1 支持集成到 Service Pack 版本中，使其可供所有客户使用。

## <a name="span-idwhat_s_new_in_windows_81_spanspan-idwhat_s_new_in_windows_81_spanwhats-new-in-windows-81"></a><span id="what_s_new_in_windows_8.1_"></span><span id="WHAT_S_NEW_IN_WINDOWS_8.1_"></span>Windows 8.1 中有哪些新功能？


Windows 8.1 包括蓝牙堆栈和相关软件的以下增强功能：

-   蓝牙版本4.0 收音机的收件箱管理控制。
-   Windows 运行时 API 支持 [**RFCOMM**](/uwp/api/Windows.Devices.Bluetooth.Rfcomm) 和 [**GATT**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile) 协议访问。

## <a name="span-idwhat_s_new_in_windows_8_spanspan-idwhat_s_new_in_windows_8_spanspan-idwhat_s_new_in_windows_8_spanwhats-new-in-windows-8"></a><span id="What_s_new_in_Windows_8_"></span><span id="what_s_new_in_windows_8_"></span><span id="WHAT_S_NEW_IN_WINDOWS_8_"></span>Windows 8 中的新增功能


Windows 8 对蓝牙堆栈和相关软件提供以下增强功能：

-   支持蓝牙版本4.0：
    -   蓝牙低能耗支持允许 Windows 与蓝牙智能外围设备连接。
    -   eL2CAP 为需要此功能的配置文件启用了增强的重新传输和流控制。
-   一种可扩展的传输模型，允许在非 USB 总线上支持蓝牙无线电收发器
-   对 HFP、A2DP 和 AVRCP 配置文件的支持

## <a name="span-idwhat_is_new_in_windows_7_spanspan-idwhat_is_new_in_windows_7_spanspan-idwhat_is_new_in_windows_7_spanwhat-is-new-in-windows-7"></a><span id="What_is_new_in_Windows_7_"></span><span id="what_is_new_in_windows_7_"></span><span id="WHAT_IS_NEW_IN_WINDOWS_7_"></span>Windows 7 中的新增功能


Windows 7 包括蓝牙堆栈和相关软件的以下增强功能：

-   支持蓝牙版本2.1：
    -   安全简单配对允许 Windows 确定要在设备之间使用的最佳配对方法，而不是要求用户进行确定。
    -   扩展查询响应允许在配对过程中更早地共享设备的友好名称。
-   改善了蓝牙设备管理的改进用户体验
-   改善了 USB 蓝牙无线电系统的安装

具有 USB \\ 类 \_ E0&子类 \_ 01&PROT 01 硬件 ID 的任何 usb 设备 \_ 都将安装为 *通用蓝牙适配器*。

## <a name="span-idwhat_is_new_in_windows_vista_spanspan-idwhat_is_new_in_windows_vista_spanspan-idwhat_is_new_in_windows_vista_spanwhat-is-new-in-windows-vista"></a><span id="What_is_new_in_Windows_Vista_"></span><span id="what_is_new_in_windows_vista_"></span><span id="WHAT_IS_NEW_IN_WINDOWS_VISTA_"></span>Windows Vista 中有哪些新功能？


Windows Vista 包括对蓝牙堆栈和相关软件的以下增强功能：

-   提高了数据速率 (EDR) 性能
-   自适应频率跳跃 (AFH) 。 此功能可改善蓝牙无线电收发器 802.11 (Wi-fi) 网络适配器的共存，这两者都在 2.4-GHz 频率范围内运行
-   面向同步连接的 (SCO) 链接支持。 对于耳机和免人工配置文件，此支持是必需的
-   内核模式设备驱动程序接口 (DDI) 对逻辑链接控制和适配协议的支持 (L2CAP) 、服务发现协议 (SDP) 和 SCO。
-   下表列出了新的蓝牙硬件 Id：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>供应商标识符 (VID) </p></td>
<td align="left"><p>产品标识符</p></td>
<td align="left"><p>描述</p></td>
</tr>
<tr class="even">
<td align="left"><p>03F0</p></td>
<td align="left"><p>011D</p></td>
<td align="left"><p>Hewlett Packard 集成蓝牙模块</p></td>
</tr>
<tr class="odd">
<td align="left"><p>03F0</p></td>
<td align="left"><p>011D&Rev_0017</p></td>
<td align="left"><p>Hewlett Packard nc4200</p></td>
</tr>
<tr class="even">
<td align="left"><p>03F0</p></td>
<td align="left"><p>171D</p></td>
<td align="left"><p>Hewlett Packard 集成蓝牙模块</p></td>
</tr>
<tr class="odd">
<td align="left"><p>03F0</p></td>
<td align="left"><p>D104</p></td>
<td align="left"><p>BT450 蓝牙无线打印机和 PC 适配器</p></td>
</tr>
<tr class="even">
<td align="left"><p>044E</p></td>
<td align="left"><p>300A</p></td>
<td align="left"><p>索尼蓝牙 USB 适配器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>044E</p></td>
<td align="left"><p>300C</p></td>
<td align="left"><p>索尼蓝牙 USB 适配器</p></td>
</tr>
<tr class="even">
<td align="left"><p>049F</p></td>
<td align="left"><p>0086</p></td>
<td align="left"><p>Hewlett Packard 集成蓝牙模块</p></td>
</tr>
<tr class="odd">
<td align="left"><p>049F</p></td>
<td align="left"><p>0086&Rev_1393</p></td>
<td align="left"><p>Hewlett Packard nx7000</p></td>
</tr>
<tr class="even">
<td align="left"><p>0930</p></td>
<td align="left"><p>0508</p></td>
<td align="left"><p>Toshiba 蓝牙适配器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0930</p></td>
<td align="left"><p>0509</p></td>
<td align="left"><p>Toshiba 蓝牙适配器</p></td>
</tr>
<tr class="even">
<td align="left"><p>0A5C</p></td>
<td align="left"><p>201E</p></td>
<td align="left"><p>IBM 集成蓝牙 IV</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0A5C</p></td>
<td align="left"><p>2110</p></td>
<td align="left"><p>ThinkPad 带 EDR 的蓝牙</p></td>
</tr>
<tr class="even">
<td align="left"><p>0B05</p></td>
<td align="left"><p>1712</p></td>
<td align="left"><p>通用蓝牙适配器</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0DB0</p></td>
<td align="left"><p>6855&Rev_2000</p></td>
<td align="left"><p> (MSI) 蓝牙设备的消息信号中断</p></td>
</tr>
<tr class="even">
<td align="left"><p>413C</p></td>
<td align="left"><p>8120</p></td>
<td align="left"><p>Dell 无线蓝牙模块</p></td>
</tr>
<tr class="odd">
<td align="left"><p>413C</p></td>
<td align="left"><p>8126</p></td>
<td align="left"><p>Dell Truemobile 355 蓝牙 + EDR</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idwhich_bluetooth_profiles_have_in-box_support_in_previous_versions_of_windows_spanspan-idwhich_bluetooth_profiles_have_in-box_support_in_previous_versions_of_windows_spanspan-idwhich_bluetooth_profiles_have_in-box_support_in_previous_versions_of_windows_spanwhich-bluetooth-profiles-have-in-box-support-in-previous-versions-of-windows"></a><span id="Which_Bluetooth_profiles_have_in-box_support_in_previous_versions_of_Windows_"></span><span id="which_bluetooth_profiles_have_in-box_support_in_previous_versions_of_windows_"></span><span id="WHICH_BLUETOOTH_PROFILES_HAVE_IN-BOX_SUPPORT_IN_PREVIOUS_VERSIONS_OF_WINDOWS_"></span>哪些蓝牙配置文件在以前版本的 Windows 中具有内置支持？


**Windows 8.1 和 Windows 8 In-Box 蓝牙配置文件**

因为 Windows 8.1、Windows 8、Windows 7 和 Windows Vista 同时为其蓝牙堆栈提供了内核模式和用户模式的编程接口，所以硬件和软件供应商可以在内核模式和用户模式下实现其他配置文件。 我们鼓励供应商通过使用合适的 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?LinkId=733613) 测试套件，并将其软件包进行数字签名，来创建此类配置文件，以测试其软件。

**Windows 7 和 Windows Vista In-Box 蓝牙配置文件**

Windows 7 和 Windows Vista 包括其他和更新的蓝牙配置文件，如下表所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">配置文件</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HID 1。1</p></td>
<td align="left"><p>人体学接口设备</p></td>
</tr>
<tr class="even">
<td align="left"><p>PANU</p></td>
<td align="left"><p>个人区域网络用户</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SPP</p></td>
<td align="left"><p>串行端口配置文件</p></td>
</tr>
<tr class="even">
<td align="left"><p>OPP</p></td>
<td align="left"><p>对象推送配置文件</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DUN</p></td>
<td align="left"><p>拨号网络</p></td>
</tr>
<tr class="even">
<td align="left"><p>HCRP</p></td>
<td align="left"><p>硬副本替换配置文件</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HFP 1。5</p></td>
<td align="left"><p>Hands-Free 配置文件</p></td>
</tr>
<tr class="even">
<td align="left"><p>A2DP 1。2</p></td>
<td align="left"><p>高级音频分发配置文件</p></td>
</tr>
<tr class="odd">
<td align="left"><p>AVRCP 1。3</p></td>
<td align="left"><p>音频/视频远程控制配置文件</p></td>
</tr>
<tr class="even">
<td align="left"><p>HOGP</p></td>
<td align="left"><p>GATT 配置文件的 HID</p></td>
</tr>
</tbody>
</table>

 

Windows 包括对以下蓝牙配置文件的内置支持：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">配置文件</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HID 1。0</p></td>
<td align="left"><p>人体学接口设备</p></td>
</tr>
<tr class="even">
<td align="left"><p>PANU</p></td>
<td align="left"><p>个人区域网络用户</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SPP</p></td>
<td align="left"><p>串行端口配置文件</p></td>
</tr>
<tr class="even">
<td align="left"><p>OPP</p></td>
<td align="left"><p>对象推送配置文件</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DUN</p></td>
<td align="left"><p>拨号网络</p></td>
</tr>
<tr class="even">
<td align="left"><p>HCRP</p></td>
<td align="left"><p>硬副本替换配置文件</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idwindows_phone_8_pics_reportspanspan-idwindows_phone_8_pics_reportspanspan-idwindows_phone_8_pics_reportspanwindows-phone-8-pics-report"></a><span id="Windows_Phone_8_PICS_report"></span><span id="windows_phone_8_pics_report"></span><span id="WINDOWS_PHONE_8_PICS_REPORT"></span>Windows Phone 8 个图片报表


可从 "蓝牙 SIG [图片值](https://go.microsoft.com/fwlink/p/?LinkId=246801) " 网页获取 Windows Phone 8) 报表 (图片的配置文件/协议实现一致性语句。

## <a name="span-iddo_users_have_to_re-pair_their_bluetooth_devices_after_they_upgrade_a_system_to_windows_81_spanspan-iddo_users_have_to_re-pair_their_bluetooth_devices_after_they_upgrade_a_system_to_windows_81_spanspan-iddo_users_have_to_re-pair_their_bluetooth_devices_after_they_upgrade_a_system_to_windows_81_spando-users-have-to-re-pair-their-bluetooth-devices-after-they-upgrade-a-system-to-windows-81"></a><span id="Do_users_have_to_re-pair_their_Bluetooth_devices_after_they_upgrade_a_system_to_Windows_8.1_"></span><span id="do_users_have_to_re-pair_their_bluetooth_devices_after_they_upgrade_a_system_to_windows_8.1_"></span><span id="DO_USERS_HAVE_TO_RE-PAIR_THEIR_BLUETOOTH_DEVICES_AFTER_THEY_UPGRADE_A_SYSTEM_TO_WINDOWS_8.1_"></span>在将系统升级到 Windows 8.1 后，用户是否必须重新配对其蓝牙设备？


如果用户从 Windows 7 升级到 Windows 8.1，则必须执行 Windows 8.1 的干净安装。 在这种情况下，必须重新安装 OEM 提供的任何蓝牙软件，并且必须重新配对所有设备。 如果用户从 Windows 8 升级到 Windows 8.1，则复杂的设备（如手机）可能需要重新配对才能重新加载第三方驱动程序。 但是，更简单的设备（例如键盘或鼠标）不需要重新配对。

因此，如果用户从 Windows 8 升级到某些设备（主要是蓝牙键盘、鼠标和音频设备） Windows 8.1，则会保留配对信息。 这可确保客户无需使用有线键盘和鼠标来升级其 Windows 版本。 他们可以使用其蓝牙键盘和鼠标来执行整个过程。

## <a name="span-idwhat_programming_interfaces_were_introduced_in_windows_81_spanspan-idwhat_programming_interfaces_were_introduced_in_windows_81_spanwhat-programming-interfaces-were-introduced-in-windows-81"></a><span id="what_programming_interfaces_were_introduced_in_windows_8.1_"></span><span id="WHAT_PROGRAMMING_INTERFACES_WERE_INTRODUCED_IN_WINDOWS_8.1_"></span>Windows 8.1 中引入了哪些编程接口？


Windows 8.1 引入了新的 Windows 运行时 Api，用于访问标准蓝牙) 上的 [**RFCOMM**](/uwp/api/Windows.Devices.Bluetooth.Rfcomm) (，以及 [**GATT**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile) (蓝牙低能耗) 。

## <a name="span-idwhat_programming_interfaces_were_introduced_in_windows_8_spanspan-idwhat_programming_interfaces_were_introduced_in_windows_8_spanspan-idwhat_programming_interfaces_were_introduced_in_windows_8_spanwhat-programming-interfaces-were-introduced-in-windows-8"></a><span id="What_programming_interfaces_were_introduced_in_Windows_8_"></span><span id="what_programming_interfaces_were_introduced_in_windows_8_"></span><span id="WHAT_PROGRAMMING_INTERFACES_WERE_INTRODUCED_IN_WINDOWS_8_"></span>Windows 8 中引入了哪些编程接口？


Windows 8 引入了新的 Api，用于通过蓝牙低能耗访问蓝牙智能外设，通过可扩展的传输模型为非 USB 蓝牙控制器创建总线驱动程序，创建增强的 L2CAP 通道。 有关这些 Api 的详细信息，请参阅 [蓝牙设备参考](https://msdn.microsoft.com/library/windows/hardware/ff536585)。

## <a name="span-idwhat_programming_interfaces_were_introduced_in_windows_7_spanspan-idwhat_programming_interfaces_were_introduced_in_windows_7_spanspan-idwhat_programming_interfaces_were_introduced_in_windows_7_spanwhat-programming-interfaces-were-introduced-in-windows-7"></a><span id="What_programming_interfaces_were_introduced_in_Windows_7_"></span><span id="what_programming_interfaces_were_introduced_in_windows_7_"></span><span id="WHAT_PROGRAMMING_INTERFACES_WERE_INTRODUCED_IN_WINDOWS_7_"></span>Windows 7 中引入了哪些编程接口？


Windows 7 引入了以前的 Api 的新 Ex 版本来提供增强的功能。 例如，BluetoothAuthenticateDeviceEx 函数允许向正在进行身份验证的设备的函数调用传递带外数据。 同样， [**BluetoothRegisterForAuthenticationEx**](/windows/win32/api/bluetoothapis/nf-bluetoothapis-bluetoothregisterforauthenticationex) 函数还包括 pin 请求和数字比较功能。 此外，当接收到发送数值比较响应的身份验证请求时，将调用 [**BluetoothSendAuthenticationResponseEx**](/windows/win32/api/bluetoothapis/nf-bluetoothapis-bluetoothsendauthenticationresponseex) 函数。 有关这些 Api 的新 Ex 版本的详细信息，请参阅 [蓝牙功能](/windows/desktop/Bluetooth/bluetooth-functions)。

## <a name="span-idwhat_programming_interfaces_were_introduced_in_windows_vista_spanspan-idwhat_programming_interfaces_were_introduced_in_windows_vista_spanspan-idwhat_programming_interfaces_were_introduced_in_windows_vista_spanwhat-programming-interfaces-were-introduced-in-windows-vista"></a><span id="What_programming_interfaces_were_introduced_in_Windows_Vista_"></span><span id="what_programming_interfaces_were_introduced_in_windows_vista_"></span><span id="WHAT_PROGRAMMING_INTERFACES_WERE_INTRODUCED_IN_WINDOWS_VISTA_"></span>Windows Vista 中引入了哪些编程接口？


Windows Vista 引入了适用于蓝牙无线技术的内核模式 DDI，提供对 SCO、SDP 和 L2CAP 的访问。 DDI 随附于 Windows 驱动程序工具包 (WDK) 版本6000，该版本随 Windows Vista 一起发布，并在以后的所有版本中生成。 我们不打算在早期版本的 Windows 上使用内核模式 DDI。 可以使用 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?LinkId=733613) 来验证内核模式蓝牙驱动程序是否符合标准驱动程序开发实践并正确使用 DDI。

Windows Vista SP2 和 Windows 7 还支持用户模式 RFComm 和蓝牙 Api。 有关详细信息，请参阅 [蓝牙设计指南](./index.md)。 WDK 包含用于新的内核模式 DDI 的文档。 有关如何下载 WDK 的详细信息，请参阅 [其他 WDK 下载](../other-wdk-downloads.md) HCK 包含有关驱动程序测试管理器 (DTM) 的文档。 有关如何下载 HCK 的详细信息，请参阅 [Windows 硬件认证工具包 (HCK) ](https://go.microsoft.com/fwlink/p/?LinkId=733613) 文档。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Windows 10 中的蓝牙支持](general-bluetooth-support-in-windows.md)

 

