---
title: 在新硬件上安装内置蓝牙驱动程序
description: 本附录介绍了在 Windows Vista 中的新硬件上安装内置 Bluetooth 驱动程序的过程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd41c40be56371a7a6f4ef7e41cf865ba68624a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798633"
---
# <a name="appendix-a-how-to-install-an-in-box-bluetooth-driver-on-new-hardware-in-windows-vista"></a>附录 A：如何在 Windows Vista 中的新硬件上安装内置的蓝牙驱动程序


本附录介绍了强制 Windows Vista 随附的蓝牙驱动程序在新的蓝牙收音机上安装的过程。 尽管有些细节有所不同，但 Windows XP SP2 使用类似的过程。

## <a name="span-idstep_1__start_device_manager_and_select_the_bluetooth_radiospanspan-idstep_1__start_device_manager_and_select_the_bluetooth_radiospanspan-idstep_1__start_device_manager_and_select_the_bluetooth_radiospanstep-1-start-device-manager-and-select-the-bluetooth-radio"></a><span id="Step_1__Start_Device_Manager_and_Select_the_Bluetooth_Radio"></span><span id="step_1__start_device_manager_and_select_the_bluetooth_radio"></span><span id="STEP_1__START_DEVICE_MANAGER_AND_SELECT_THE_BLUETOOTH_RADIO"></span>步骤1：启动设备管理器并选择蓝牙收音机


开始设备管理器：

1.  选择 " **开始**"，导航到 "所有程序" "附件" " **&gt; &gt; 命令提示符**"，选择并按住 (或右键单击) **命令提示符**"，然后选择并按住 (或右键单击) " 以 **管理员身份运行** "以使用提升的权限打开命令窗口。
2.  键入以下内容： **devmgmt.msc**

在 " **其他设备**" 下的 "设备管理器设备列表中找到蓝牙收音机的条目。 在下图中，无线电的名称为 "UGT"。 在某些便携式计算机上，可能需要先使用组合键（如 Fn + F5）来打开蓝牙收音机。

![屏幕截图显示 "设备管理器" 右键单击 "U G T" 并单击 "更新驱动程序软件 ..."选择.](images/bthnewhwstep1.jpg)

若要验证所选设备是否为蓝牙无线电，请选择并按住 (或右键单击) 设备名称，然后选择 " **属性** " 以显示 " **属性** " 对话框。 在 " **详细信息** " 选项卡上，验证设备是否具有蓝牙无线电的兼容 ID：

USB \\ 类 \_ E0&子类 \_ 01&Prot \_ 01
### <a name="span-idstep_2__start_the_update_driver_software_wizardspanspan-idstep_2__start_the_update_driver_software_wizardspanspan-idstep_2__start_the_update_driver_software_wizardspanstep-2-start-the-update-driver-software-wizard"></a><span id="Step_2__Start_the_Update_Driver_Software_Wizard"></span><span id="step_2__start_the_update_driver_software_wizard"></span><span id="STEP_2__START_THE_UPDATE_DRIVER_SOFTWARE_WIZARD"></span>步骤2：启动更新驱动程序软件向导

选择并按住 (或右键单击蓝牙单选节点) ，然后选择 " **更新驱动程序软件**"。 若要转到下图中的页面，请选择 **"浏览计算机以查找驱动程序软件**"。 若要手动选择驱动程序，请选择 " **让我从计算机上的设备驱动程序列表中** 选择"。

![显示 "更新驱动程序软件-U G T" 窗口的屏幕截图。](images/bthnewhwstep2.jpg)

### <a name="span-idstep_3__select_the_generic_bluetooth_driverspanspan-idstep_3__select_the_generic_bluetooth_driverspanspan-idstep_3__select_the_generic_bluetooth_driverspanstep-3-select-the-generic-bluetooth-driver"></a><span id="Step_3__Select_the_Generic_Bluetooth_Driver"></span><span id="step_3__select_the_generic_bluetooth_driver"></span><span id="STEP_3__SELECT_THE_GENERIC_BLUETOOTH_DRIVER"></span>步骤3：选择通用蓝牙驱动程序

更新驱动程序软件向导接下来显示可用驱动程序的列表。 选择 " **蓝牙无线电收发** 器"，然后选择与系统匹配的蓝牙无线电，如下图所示。 如果不确定要使用的驱动程序，可以使用通用驱动程序进行测试。 为此，请选择 " **通用适配器** 作为制造商"，并选择 **通用蓝牙适配器** 作为 "型号"。

![屏幕截图，显示在 "模型" 窗格中选择 "通用蓝牙适配器" 的 "更新驱动程序软件-U G T" 窗口。](images/bthnewhwstep3.jpg)

选择驱动程序后，向导会要求你确认是否要在新的蓝牙无线电上安装指定的驱动程序。 如果尝试在非蓝牙无线电设备上安装蓝牙驱动程序，该驱动程序可能不会启动。

如果驱动程序加载正确，设备管理器应在蓝牙无线电节点下有一个通用的蓝牙适配器项，如下图所示。

![蓝牙更新驱动程序软件 vista](images/bthnewhwstep4.jpg)

如果驱动程序无法启动，例如 Windows 返回了开始错误代码，请检查事件日志以帮助确定原因。

 

 





