---
title: 蓝牙用户界面
description: 说明如何使用 Windows 中的蓝牙用户界面的软件开发人员和供应商
ms.assetid: 7E342615-217A-4252-AAC4-7F7EE013840D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc4ad313beb432d5d92688f034b6c9a97ddb3160
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354036"
---
# <a name="bluetooth-user-interface"></a>蓝牙用户界面


## <a name="span-idwhatisthebluetoothfiletransferwizardspanspan-idwhatisthebluetoothfiletransferwizardspanspan-idwhatisthebluetoothfiletransferwizardspanwhat-is-the-bluetooth-file-transfer-wizard"></a><span id="What_is_the_Bluetooth_File_Transfer_Wizard_"></span><span id="what_is_the_bluetooth_file_transfer_wizard_"></span><span id="WHAT_IS_THE_BLUETOOTH_FILE_TRANSFER_WIZARD_"></span>什么是 Bluetooth 文件传输向导？


蓝牙文件传输向导使用户能够在计算机和蓝牙设备之间传输文件。 例如，用户可以在计算机和移动电话或个人数字助理 (PDA) 之间传输文件。 蓝牙文件传输向导还可以支持蓝牙的两台计算机之间传输文件。

**请注意**  Fsquirt.exe 文件中实现 GUI 蓝牙文件传输向导将使用默认值。 此文件可以是从基础传输向导机制来启用替换默认蓝牙文件传输向导 GUI 中解除挂钩。 有关详细信息，请参阅下面的问题。

 

## <a name="span-idhowdoiunhookfsquirtexespanspan-idhowdoiunhookfsquirtexespanhow-do-i-unhook-fsquirtexe"></a><span id="how_do_i_unhook_fsquirt.exe_"></span><span id="HOW_DO_I_UNHOOK_FSQUIRT.EXE_"></span>如何解除挂钩 Fsquirt.exe？


将替换的专有应用程序为内置蓝牙文件传输向导所需的软件开发人员可以解除 Fsquirt.exe 挂钩从基础传输向导机制，通过执行以下步骤：

1.  创建名为的 DWORD 值**DisableFsquirt** HKLM 下\\系统\\CurrentControlSet\\Services\\Bthport\\Parameters 项在注册表中的。
2.  设置的值**DisableFsquirt**为 0x1
3.  重新启动或在命令提示符窗口中运行以下命令： **fsquirt.exe-取消注册**

若要重新启用 Fsquirt.exe，请执行以下步骤：

1.  删除**DisableFsquirt**注册表中的值。
2.  重新启动或在命令提示符窗口中运行以下命令： **fsquirt.exe-注册**

## <a name="span-idinwindowsvistawhydoesthebluetoothnotificationareaiconsometimesdisappearspanspan-idinwindowsvistawhydoesthebluetoothnotificationareaiconsometimesdisappearspanspan-idinwindowsvistawhydoesthebluetoothnotificationareaiconsometimesdisappearspanin-windows-vista-why-does-the-bluetooth-notification-area-icon-sometimes-disappear"></a><span id="In_Windows_Vista__why_does_the_Bluetooth_notification_area_icon_sometimes_disappear_"></span><span id="in_windows_vista__why_does_the_bluetooth_notification_area_icon_sometimes_disappear_"></span><span id="IN_WINDOWS_VISTA__WHY_DOES_THE_BLUETOOTH_NOTIFICATION_AREA_ICON_SOMETIMES_DISAPPEAR_"></span>在 Windows Vista 中，为什么 does 蓝牙通知区域图标有时消失？


在 Windows Vista RTM 和 Windows Vista SP1，蓝牙无线连接到计算机时，将出现蓝牙通知区域图标。 图标配置为将保持活动状态最多 10 分钟，但在该时间段后，图标消失从通知区域。

如果用户想持久的蓝牙通知区域图标，他们可以选择**在通知区域中显示的蓝牙图标**上的复选框**选项**控制面板蓝牙设置选项卡应用程序。

![蓝牙通知设置](images/bluetoothnotificationsettings.jpg)

**请注意**  即使没有蓝牙图标是在通知区域中，您仍可以使用控制面板蓝牙设置应用程序执行相关的任务，如添加新的蓝牙设备，使计算机容易被发现，依此类推。

 

## <a name="span-idcanvendorsaddtabstothecontrolpanelbluetoothsettingsapplicationspanspan-idcanvendorsaddtabstothecontrolpanelbluetoothsettingsapplicationspanspan-idcanvendorsaddtabstothecontrolpanelbluetoothsettingsapplicationspancan-vendors-add-tabs-to-the-control-panel-bluetooth-settings-application"></a><span id="Can_vendors_add_tabs_to_the_Control_Panel_Bluetooth_Settings_application_"></span><span id="can_vendors_add_tabs_to_the_control_panel_bluetooth_settings_application_"></span><span id="CAN_VENDORS_ADD_TABS_TO_THE_CONTROL_PANEL_BLUETOOTH_SETTINGS_APPLICATION_"></span>供应商是否可以将选项卡添加到控制面板蓝牙设置应用程序？


是的供应商可以通过实现应用程序 shell 属性页处理程序添加选项卡。 例如，Ihv 现成 Bluetooth 堆栈实现扩展可以实现的属性表处理程序添加配置文件的文件传输，例如添加到版本 2.1 蓝牙规范和等等的增强功能的选项卡。 有关如何实现属性页处理程序的详细信息，请参阅[属性页处理程序](https://docs.microsoft.com/previous-versions/windows/desktop/legacy/cc144106(v=vs.85))。

## <a name="span-idwhydoeswindows7andwindowsvistadisplayadialogboxwhenabluetoothaudiodeviceisinitiallyconnectedspanspan-idwhydoeswindows7andwindowsvistadisplayadialogboxwhenabluetoothaudiodeviceisinitiallyconnectedspanspan-idwhydoeswindows7andwindowsvistadisplayadialogboxwhenabluetoothaudiodeviceisinitiallyconnectedspanwhy-does-windows-7-and-windows-vista-display-a-dialog-box-when-a-bluetooth-audio-device-is-initially-connected"></a><span id="Why_does_Windows_7_and_Windows_Vista_display_a_dialog_box_when_a_Bluetooth_audio_device_is_initially_connected_"></span><span id="why_does_windows_7_and_windows_vista_display_a_dialog_box_when_a_bluetooth_audio_device_is_initially_connected_"></span><span id="WHY_DOES_WINDOWS_7_AND_WINDOWS_VISTA_DISPLAY_A_DIALOG_BOX_WHEN_A_BLUETOOTH_AUDIO_DEVICE_IS_INITIALLY_CONNECTED_"></span>为什么 Windows 7 和 Windows Vista 显示一个对话框时蓝牙音频设备最初要连接？


Windows 可能会为耳机 (HSP)，无需手动 (HFP)，提供默认支持或高级音频分发 (A2DP) 音频配置文件。 如果使用不具有必要的驱动程序的系统配对蓝牙音频设备，则 Windows 通常会显示**发现新硬件**对话框。 但是，如果以下项之一为 true，也不会显示对话框中：

-   计算机的 OEM 提供支持蓝芽音频的配置文件包。
-   最终用户之前安装蓝牙耳机和 IHV 或 Windows Update 提供的媒体从下载的音频驱动程序。

## <a name="span-idhowdoienhancethefunctionalityandbetterrepresentmybluetoothdeviceindevicesandprintersspanspan-idhowdoienhancethefunctionalityandbetterrepresentmybluetoothdeviceindevicesandprintersspanspan-idhowdoienhancethefunctionalityandbetterrepresentmybluetoothdeviceindevicesandprintersspanhow-do-i-enhance-the-functionality-and-better-represent-my-bluetooth-device-in-devices-and-printers"></a><span id="How_do_I_enhance_the_functionality_and_better_represent_my_Bluetooth_device_in_Devices_and_Printers_"></span><span id="how_do_i_enhance_the_functionality_and_better_represent_my_bluetooth_device_in_devices_and_printers_"></span><span id="HOW_DO_I_ENHANCE_THE_FUNCTIONALITY_AND_BETTER_REPRESENT_MY_BLUETOOTH_DEVICE_IN_DEVICES_AND_PRINTERS_"></span>如何增强的功能和更好地表示 Bluetooth 的设备中设备和打印机？


可以为您的 Bluetooth 设备创建设备元数据包，以便设备和打印机显示有关你的设备，如图像逼真的图标和自定义说明特定于设备的信息。 这可以显著提高蓝牙设备的用户的体验。 例如，你可能想要更有效地公开你的设备支持的所有功能。 某些设备类还可以利用设备阶段，允许 Ihv 通过提供的自定义和全新的特定于设备的用户界面来进一步增强设备体验。

有关如何创建设备的设备元数据包的详细信息，请参阅[如何为设备和打印机创建设备元数据包](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/)。

有关设备阶段的详细信息，请参阅 **"设备阶段常规开发工具包"MSDN 网站上**。

**请注意**  以充分利用设备阶段，设备 ID 配置文件必须实现，其中包括硬件 ID、 供应商 ID 和 PID。

 

 

 





