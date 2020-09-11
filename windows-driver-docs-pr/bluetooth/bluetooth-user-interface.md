---
title: 蓝牙用户界面
description: 介绍如何在 Windows 中使用适用于软件开发人员和供应商的蓝牙用户界面
ms.assetid: 7E342615-217A-4252-AAC4-7F7EE013840D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19ec126bc62768458d6a5eab14b6244fd4ddf57c
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009999"
---
# <a name="bluetooth-user-interface"></a>蓝牙用户界面


## <a name="span-idwhat_is_the_bluetooth_file_transfer_wizard_spanspan-idwhat_is_the_bluetooth_file_transfer_wizard_spanspan-idwhat_is_the_bluetooth_file_transfer_wizard_spanwhat-is-the-bluetooth-file-transfer-wizard"></a><span id="What_is_the_Bluetooth_File_Transfer_Wizard_"></span><span id="what_is_the_bluetooth_file_transfer_wizard_"></span><span id="WHAT_IS_THE_BLUETOOTH_FILE_TRANSFER_WIZARD_"></span>什么是蓝牙文件传输向导？


蓝牙文件传输向导允许用户在计算机和 Bluetooth 设备之间传输文件。 例如，用户可以在计算机与移动电话或个人数字助理 (PDA) 之间传输文件。 蓝牙文件传输向导还可以在支持蓝牙的两台计算机之间传输文件。

**注意**   蓝牙文件传输向导使用的默认 GUI 在 Fsquirt.exe 文件中实现。 此文件可从基础传输向导机制中解除挂钩，以启用默认蓝牙文件传输向导 GUI 的替换。 有关详细信息，请参阅以下问题。

 

## <a name="span-idhow_do_i_unhook_fsquirtexe_spanspan-idhow_do_i_unhook_fsquirtexe_spanhow-do-i-unhook-fsquirtexe"></a><span id="how_do_i_unhook_fsquirt.exe_"></span><span id="HOW_DO_I_UNHOOK_FSQUIRT.EXE_"></span>如何实现解除挂钩 Fsquirt.exe？


需要将内置蓝牙文件传输向导替换为专有应用程序的软件开发人员可以执行以下步骤，将 Fsquirt.exe 从基础传输向导机制中解除挂钩：

1.  在注册表中的 HKLM **DisableFsquirt** \\ System \\ CurrentControlSet \\ Services \\ Bthport \\ Parameters 项下，创建一个名为 DisableFsquirt 的 DWORD 值。
2.  将 **DisableFsquirt** 的值设置为0x1
3.  重新启动或在命令提示符窗口中运行以下命令： **fsquirt.exe-注销**

若要重新启用 Fsquirt.exe，请执行以下步骤：

1.  从注册表中删除 **DisableFsquirt** 值。
2.  重新启动或在命令提示符窗口中运行以下命令： **fsquirt.exe-Register**

## <a name="span-idin_windows_vista__why_does_the_bluetooth_notification_area_icon_sometimes_disappear_spanspan-idin_windows_vista__why_does_the_bluetooth_notification_area_icon_sometimes_disappear_spanspan-idin_windows_vista__why_does_the_bluetooth_notification_area_icon_sometimes_disappear_spanin-windows-vista-why-does-the-bluetooth-notification-area-icon-sometimes-disappear"></a><span id="In_Windows_Vista__why_does_the_Bluetooth_notification_area_icon_sometimes_disappear_"></span><span id="in_windows_vista__why_does_the_bluetooth_notification_area_icon_sometimes_disappear_"></span><span id="IN_WINDOWS_VISTA__WHY_DOES_THE_BLUETOOTH_NOTIFICATION_AREA_ICON_SOMETIMES_DISAPPEAR_"></span>在 Windows Vista 中，为什么蓝牙通知区域图标有时会消失？


在 Windows Vista RTM 和带 SP1 的 Windows Vista 中，当蓝牙无线电连接到计算机时，将显示 "蓝牙通知区域" 图标。 图标配置为保持活动状态长达10分钟，但在该时间段后，该图标将从通知区域中消失。

如果用户需要永久的蓝牙通知区域图标，则他们可以在 "控制面板" 的 "蓝牙设置" 应用程序的 "**选项**" 选项卡上选中 "在**通知区域中显示蓝牙图标**" 复选框。

![蓝牙通知设置](images/bluetoothnotificationsettings.jpg)

**注意**   即使通知区域中没有蓝牙图标，你仍可以使用 "控制面板" 的 "蓝牙设置" 应用程序来执行相关任务，如添加新的蓝牙设备、使计算机可发现等。

 

## <a name="span-idcan_vendors_add_tabs_to_the_control_panel_bluetooth_settings_application_spanspan-idcan_vendors_add_tabs_to_the_control_panel_bluetooth_settings_application_spanspan-idcan_vendors_add_tabs_to_the_control_panel_bluetooth_settings_application_spancan-vendors-add-tabs-to-the-control-panel-bluetooth-settings-application"></a><span id="Can_vendors_add_tabs_to_the_Control_Panel_Bluetooth_Settings_application_"></span><span id="can_vendors_add_tabs_to_the_control_panel_bluetooth_settings_application_"></span><span id="CAN_VENDORS_ADD_TABS_TO_THE_CONTROL_PANEL_BLUETOOTH_SETTINGS_APPLICATION_"></span>供应商能否将选项卡添加到控制面板的 "蓝牙设置" 应用程序？


是的，供应商可以通过为应用程序实现 shell 属性表处理程序来添加选项卡。 例如，实现对内置蓝牙堆栈的扩展的 Ihv 可以实现属性表处理程序，该处理程序可为配置文件（如文件传输）、增强版本2.1 的蓝牙规范等添加选项卡。 有关如何实现属性表处理程序的详细信息，请参阅 [属性表处理程序](/previous-versions/windows/desktop/legacy/cc144106(v=vs.85))。

## <a name="span-idwhy_does_windows_7_and_windows_vista_display_a_dialog_box_when_a_bluetooth_audio_device_is_initially_connected_spanspan-idwhy_does_windows_7_and_windows_vista_display_a_dialog_box_when_a_bluetooth_audio_device_is_initially_connected_spanspan-idwhy_does_windows_7_and_windows_vista_display_a_dialog_box_when_a_bluetooth_audio_device_is_initially_connected_spanwhy-does-windows-7-and-windows-vista-display-a-dialog-box-when-a-bluetooth-audio-device-is-initially-connected"></a><span id="Why_does_Windows_7_and_Windows_Vista_display_a_dialog_box_when_a_Bluetooth_audio_device_is_initially_connected_"></span><span id="why_does_windows_7_and_windows_vista_display_a_dialog_box_when_a_bluetooth_audio_device_is_initially_connected_"></span><span id="WHY_DOES_WINDOWS_7_AND_WINDOWS_VISTA_DISPLAY_A_DIALOG_BOX_WHEN_A_BLUETOOTH_AUDIO_DEVICE_IS_INITIALLY_CONNECTED_"></span>为什么当蓝牙音频设备最初连接时，Windows 7 和 Windows Vista 会显示一个对话框？


Windows 可能不提供对耳机 (HSP) 、免提 (HFP) 或高级音频分发 (A2DP) 音频配置文件的默认支持。 如果蓝牙音频设备与没有必需驱动程序的系统配对，则 Windows 通常会显示 " **发现新硬件** " 对话框。 但是，如果满足以下条件之一，则不会显示该对话框：

-   计算机的 OEM 提供了支持蓝牙音频的配置文件包。
-   最终用户以前安装了 Bluetooth 耳机，并从安装了 IHV 或 Windows 更新的媒体下载了音频驱动程序。

## <a name="span-idhow_do_i_enhance_the_functionality_and_better_represent_my_bluetooth_device_in_devices_and_printers_spanspan-idhow_do_i_enhance_the_functionality_and_better_represent_my_bluetooth_device_in_devices_and_printers_spanspan-idhow_do_i_enhance_the_functionality_and_better_represent_my_bluetooth_device_in_devices_and_printers_spanhow-do-i-enhance-the-functionality-and-better-represent-my-bluetooth-device-in-devices-and-printers"></a><span id="How_do_I_enhance_the_functionality_and_better_represent_my_Bluetooth_device_in_Devices_and_Printers_"></span><span id="how_do_i_enhance_the_functionality_and_better_represent_my_bluetooth_device_in_devices_and_printers_"></span><span id="HOW_DO_I_ENHANCE_THE_FUNCTIONALITY_AND_BETTER_REPRESENT_MY_BLUETOOTH_DEVICE_IN_DEVICES_AND_PRINTERS_"></span>如何实现增强功能并更好地表示设备和打印机中的蓝牙设备？


可以为 Bluetooth 设备创建设备元数据包，使设备和打印机显示设备特定的信息，例如，照片的图标和自定义说明。 这可以显著提高用户对蓝牙设备的体验。 例如，你可能希望更有效地公开设备支持的所有功能。 某些设备类还可以利用设备阶段，通过提供自定义的特定于设备的用户界面，使 Ihv 进一步增强设备体验。

有关如何为设备创建设备元数据包的详细信息，请参阅如何为设备 [和打印机创建设备元数据包](/previous-versions/windows/hardware/metadata/)。

有关设备阶段的详细信息，请参阅 **MSDN 网站上的 "设备阶段通用开发工具包"**。

**注意**   若要利用设备阶段，必须实现设备 ID 配置文件，其中包括硬件 ID、供应商 ID 和 PID。

 

 

