---
title: 蓝牙常见问题解答
description: 此常见问题部分提供有关 Windows 操作系统系列的蓝牙无线技术支持信息。
ms.assetid: 529DD4A2-4E4B-47F4-BD65-BE89EA21E217
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c18d2e9d8420c09dfb2bf3d8cc890dd77a59454c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328311"
---
# <a name="bluetooth-faq"></a>蓝牙常见问题解答


此常见问题部分提供有关 Windows 操作系统系列的蓝牙无线技术支持信息。 它是主要面向独立硬件供应商 (Ihv) 的新硬件和软件开发人员感兴趣的 Windows 和地址主题上的蓝牙生态系统。

以下主题中的位置附加常见问题：

[蓝牙版本和配置文件支持在 Windows 10](general-bluetooth-support-in-windows.md)
[蓝牙版本和配置文件支持在以前的 Windows 版本](bluetooth-support-in-previous-windows-versions.md)
[蓝牙主机单选支持](bluetooth-host-radio-support.md) 
[蓝牙用户界面](bluetooth-user-interface.md)
[蓝牙认证](bluetooth-certification.md)
[附录 A](bluetooth-faq--appendix-a.md) 
[附录 B](bluetooth-faq--appendix-b.md)
## <a name="span-idhowmanybluetoothradioscanwindowssupportspanspan-idhowmanybluetoothradioscanwindowssupportspanspan-idhowmanybluetoothradioscanwindowssupportspanhow-many-bluetooth-radios-can-windows-support"></a><span id="How_many_Bluetooth_radios_can_Windows_support_"></span><span id="how_many_bluetooth_radios_can_windows_support_"></span><span id="HOW_MANY_BLUETOOTH_RADIOS_CAN_WINDOWS_SUPPORT_"></span>多少 Bluetooth 无线电收发器可以 Windows 支持？


在 Windows 中的 Bluetooth 堆栈支持只有一个蓝牙无线功能。 此单选必须遵守蓝牙规范和最新的 Windows 硬件认证计划要求。

## <a name="span-idhowcanbluetoothandwi-firadioscoexisteffectivelyspanspan-idhowcanbluetoothandwi-firadioscoexisteffectivelyspanspan-idhowcanbluetoothandwi-firadioscoexisteffectivelyspanhow-can-bluetooth-and-wi-fi-radios-coexist-effectively"></a><span id="How_can_Bluetooth_and_Wi-Fi_radios_coexist_effectively_"></span><span id="how_can_bluetooth_and_wi-fi_radios_coexist_effectively_"></span><span id="HOW_CAN_BLUETOOTH_AND_WI-FI_RADIOS_COEXIST_EFFECTIVELY_"></span>如何可以蓝牙和 Wi-fi 无线电收发器有效地共存？


蓝牙和 Wi-fi 无线电收发器工作在 2.4 GHz 频率范围内，因此它们无法立即尝试使用相同的频率。 跳跃窗口的技术，Bluetooth 无线技术使用的频率可以防止此类冲突导致完成连接丢失，但它可能会减少这两个无线电收发器的传输速率。

蓝牙规范的 2.0 版支持 AFH。 使用 AFH，蓝牙无线感测到来自其他类型的无线收发器的流量、 将标记为"干扰"的忙通道和避免这些通道，如跃点的频率。 Windows Vista 和更高版本可以 AFH 进一步提高通过将视为可共享范围的"无线方式"。 此功能使无线技术，比如 Wi-fi 适配器报告他们想要使用的通道。 当 Bluetooth 堆栈将变为活动状态时，它将通知的报告中使用通道，并将其标记为存在干扰。

## <a name="span-idhowdoienableafhinwindowsspanspan-idhowdoienableafhinwindowsspanspan-idhowdoienableafhinwindowsspanhow-do-i-enable-afh-in-windows"></a><span id="How_do_I_enable_AFH_in_Windows_"></span><span id="how_do_i_enable_afh_in_windows_"></span><span id="HOW_DO_I_ENABLE_AFH_IN_WINDOWS_"></span>如何启用 Windows 中的 AFH？


Windows Vista 和更高版本包括一个共享且开源的特点模型以支持基于版本 2.0 和更高版本的蓝牙规范的 Bluetooth 无线电收发器 AFH。 但是，默认情况下禁用此功能。 对于以支持共享的范围模型的系统，OEM 必须显式启用该功能，并指定频率带区应阻止围绕活动的 Wi-fi 通道的宽度。 若要指定频率带区的宽度，请创建类型 REG 值\_ChannelAvoidanceRange 名为以下注册表项下的 DWORD:

**HKLM\\System\\CurrentControlSet\\Services\\BthServ\\Parameters**

**ChannelAvoidanceRange**值启用或禁用范围共享，并指定阻止的频率带区的宽度。 若要启用范围共享，请设置**ChannelAvoidanceRange**到频率带区应阻止围绕活动的 Wi-fi 通道的整个宽度。 单位是以 mhz 为单位，范围可以介于 20 到 40 (0.02 到 0.04 GHz)。 Oem 必须确定合适的带宽，根据所选的一组无线收发器、 天线特征和单选制造商反馈。

一个新**ChannelAvoidanceRange**值仅后重新启动系统时，才会生效。 理想情况下，应设置 OEM **ChannelAvoidanceRange**在预安装过程中的值。

对于要高效地工作的 Windows 共享范围模型，Wi-fi 微型端口驱动程序必须对网络的连接管理器报告其通道使用情况。 然后，网络堆栈将通道使用的信息传递给 Bluetooth 堆栈。

## <a name="span-idhowdoienableremotewakeinwindowsspanspan-idhowdoienableremotewakeinwindowsspanspan-idhowdoienableremotewakeinwindowsspanhow-do-i-enable-remote-wake-in-windows"></a><span id="How_do_I_enable_remote_wake_in_Windows_"></span><span id="how_do_i_enable_remote_wake_in_windows_"></span><span id="HOW_DO_I_ENABLE_REMOTE_WAKE_IN_WINDOWS_"></span>如何启用 Windows 中的远程唤醒？


Windows Vista Service Pack 2 (SP2) 和更高版本提供了软件支持，允许已启用蓝牙的键盘和鼠标设备唤醒计算机从睡眠状态 (S3) 或休眠状态 (S4) 的系统电源状态。 此类唤醒才能成功，蓝牙模块必须自供电，并且必须具有足够的电源来唤醒计算机。 即使 Windows 允许唤醒从 S4 系统电源状态，如果蓝牙模块未通电 S4 计算机时，将无法唤醒计算机。

若要在软件中启用远程唤醒，验证蓝牙模块可以支持唤醒并设置以下注册表值：

-   HKLM\\系统\\CurrentControlSet\\Services\\Bthport\\参数\\SystemRemoteWakeSupported:(DWORD) 1
-   HKLM\\系统\\CurrentControlSet\\Enum\\USB\\&lt;vid\_pid&gt;\\&lt;Bluetooth 无线电 ID&gt;\\设备参数\\RemoteWakeEnabled:(DWORD) 1
-   HKLM\\系统\\CurrentControlSet\\Enum\\USB\\&lt;vid\_pid&gt;\\&lt;Bluetooth 无线电 ID&gt;\\设备参数\\DeviceRemoteWakeSupported:(DWORD) 1

**请注意**  蓝牙无线属性页在设备管理器是否**电源管理**选项卡上，单选可以支持唤醒。 如果没有**电源管理**选项卡存在，单选可能支持唤醒，但不太可能。

 

 

 





