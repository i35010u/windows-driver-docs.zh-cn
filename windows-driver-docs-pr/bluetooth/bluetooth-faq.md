---
title: 蓝牙常见问题解答
description: 此 FAQ 部分提供有关 Windows 操作系统系列的蓝牙无线技术支持的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e63ec9276ebd73aedeeee3e5563afa75eaa00330
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784233"
---
# <a name="bluetooth-faq"></a>蓝牙常见问题解答


此 FAQ 部分提供有关 Windows 操作系统系列的蓝牙无线技术支持的信息。 它主要用于独立的硬件供应商 (Ihv) Windows 上的蓝牙生态系统的新手，并提供对硬件和软件开发人员感兴趣的主题。

其他常见问题位于以下主题中：

[Windows 10 中的蓝牙版本和配置文件支持](general-bluetooth-support-in-windows.md) 
[以前的 Windows 版本中的蓝牙版本和配置文件支持](bluetooth-support-in-previous-windows-versions.md) 
[蓝牙主机无线电支持](bluetooth-host-radio-support.md) 
[蓝牙用户界面](bluetooth-user-interface.md) 
[蓝牙认证](bluetooth-certification.md) 
[附录 A](bluetooth-faq--appendix-a.md) 
[附录 B](bluetooth-faq--appendix-b.md)
## <a name="span-idhow_many_bluetooth_radios_can_windows_support_spanspan-idhow_many_bluetooth_radios_can_windows_support_spanspan-idhow_many_bluetooth_radios_can_windows_support_spanhow-many-bluetooth-radios-can-windows-support"></a><span id="How_many_Bluetooth_radios_can_Windows_support_"></span><span id="how_many_bluetooth_radios_can_windows_support_"></span><span id="HOW_MANY_BLUETOOTH_RADIOS_CAN_WINDOWS_SUPPORT_"></span>Windows 支持多少个蓝牙无线电收发器？


Windows 中的蓝牙堆栈仅支持一个蓝牙收音机。 此无线电必须符合蓝牙规范和最新的 Windows 硬件认证计划要求。

## <a name="span-idhow_can_bluetooth_and_wi-fi_radios_coexist_effectively_spanspan-idhow_can_bluetooth_and_wi-fi_radios_coexist_effectively_spanspan-idhow_can_bluetooth_and_wi-fi_radios_coexist_effectively_spanhow-can-bluetooth-and-wi-fi-radios-coexist-effectively"></a><span id="How_can_Bluetooth_and_Wi-Fi_radios_coexist_effectively_"></span><span id="how_can_bluetooth_and_wi-fi_radios_coexist_effectively_"></span><span id="HOW_CAN_BLUETOOTH_AND_WI-FI_RADIOS_COEXIST_EFFECTIVELY_"></span>蓝牙和 Wi-Fi 无线功能如何有效地共存？


蓝牙和 Wi-Fi 无线收发器都在 2.4-GHz 频率范围内运行，因此它们可以暂时尝试使用相同的频率。 Bluetooth 无线技术使用的频率跳跃技术可防止这种冲突导致完全的连接丢失，但这可能降低两个无线收发器的传输速率。

蓝牙规范2.0 版支持 AFH。 使用 AFH，蓝牙无线电可感知来自其他类型收音机的流量，将繁忙通道标记为 "干扰"，并在其跃点时避免使用这些通道。 Windows Vista 和更高版本通过将 "air" 视为可共享的光谱，进一步改善了 AFH。 此功能使无线技术（例如 Wi-Fi 适配器）报告他们要使用哪些通道。 当蓝牙堆栈变为活动状态时，它会通知所报告的使用通道，并将其标记为干扰。

## <a name="span-idhow_do_i_enable_afh_in_windows_spanspan-idhow_do_i_enable_afh_in_windows_spanspan-idhow_do_i_enable_afh_in_windows_spanhow-do-i-enable-afh-in-windows"></a><span id="How_do_I_enable_AFH_in_Windows_"></span><span id="how_do_i_enable_afh_in_windows_"></span><span id="HOW_DO_I_ENABLE_AFH_IN_WINDOWS_"></span>如何实现在 Windows 中启用 AFH？


Windows Vista 和更高版本包含共享的模型，以支持基于版本2.0 和更高版本的蓝牙规范的蓝牙无线电收发器的 AFH。 但是，默认情况下禁用此功能。 为了使系统支持共享频谱模型，OEM 必须显式启用该功能，并指定应在活动 Wi-fi 通道周围阻止的频带的宽度。 若要指定 frequency 的宽度，请 \_ 在以下注册表项下创建名为 ChannelAvoidanceRange 的类型为 REG DWORD 的值：

**HKLM \\ System \\ CurrentControlSet \\ Services \\ BthServ \\ 参数**

**ChannelAvoidanceRange** 值启用或禁用彩虹共享，并指定阻止的频带的宽度。 若要启用光谱共享，请将 **ChannelAvoidanceRange** 设置为应在活动 Wi-Fi 通道周围阻止的频带的整个宽度。 单位为 MHz，范围为20到 40 (0.02 到 0.04 GHz) 。 Oem 必须根据一组选定的无线电、天线特征和无线电制造商反馈来确定合适的带宽。

仅当系统重新启动后，新的 **ChannelAvoidanceRange** 值才会生效。 理想情况下，OEM 应在预安装过程中设置 **ChannelAvoidanceRange** 值。

要使 Windows 共享级模型有效工作，Wi-Fi 微型端口驱动程序必须向网络连接管理器报告其通道使用情况。 然后，网络堆栈会将通道使用信息传递到蓝牙堆栈。

## <a name="span-idhow_do_i_enable_remote_wake_in_windows_spanspan-idhow_do_i_enable_remote_wake_in_windows_spanspan-idhow_do_i_enable_remote_wake_in_windows_spanhow-do-i-enable-remote-wake-in-windows"></a><span id="How_do_I_enable_remote_wake_in_Windows_"></span><span id="how_do_i_enable_remote_wake_in_windows_"></span><span id="HOW_DO_I_ENABLE_REMOTE_WAKE_IN_WINDOWS_"></span>如何实现在 Windows 中启用远程唤醒？


带有 Service Pack 2 (SP2) 和更高版本的 Windows Vista 提供的软件支持可让启用 Bluetooth 的键盘和鼠标设备将计算机从睡眠 (S3) 或休眠 (S4) 系统电源状态唤醒。 为了使这种唤醒成功，蓝牙模块必须具有自供电模式，并且必须具有足够的能力唤醒计算机。 即使 Windows 启用了从 S4 系统电源状态的唤醒功能，如果在计算机处于 S4 中时蓝牙模块不能通电，计算机也无法唤醒。

若要启用软件远程唤醒，请验证蓝牙模块是否可以支持唤醒，并设置以下注册表值：

-   HKLM \\ System \\ CurrentControlSet \\ Services \\ Bthport \\ Parameters \\ SystemRemoteWakeSupported： (DWORD) 1
-   HKLM \\ 系统 \\ CurrentControlSet \\ 枚举 \\ USB \\ &lt; vid \_ pid &gt; \\ &lt; Bluetooth 收音机 ID &gt; \\ 设备参数 \\ RemoteWakeEnabled： (DWORD) 1
-   HKLM \\ 系统 \\ CurrentControlSet \\ 枚举 \\ USB \\ &lt; vid \_ pid &gt; \\ &lt; Bluetooth 收音机 ID &gt; \\ 设备参数 \\ DeviceRemoteWakeSupported： (DWORD) 1

**注意**  如果设备管理器中的蓝牙无线电属性页具有 " **电源管理** " 选项卡，则该无线电可以支持唤醒。 如果不存在 " **电源管理** " 选项卡，则无线电可能支持唤醒，但不太可能。

 

 

 





