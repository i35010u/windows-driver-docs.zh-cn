---
title: 安装新硬件上的框中的蓝牙驱动程序
description: 本附录介绍了 Windows Vista 中的新硬件上安装内置的蓝牙驱动程序的过程
ms.assetid: 399514FD-2BD8-4DC2-8446-F5EEB4120876
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1dc6e19d5f4a7a15537c109fd9d4a92592ed93b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328334"
---
# <a name="appendix-a-how-to-install-an-in-box-bluetooth-driver-on-new-hardware-in-windows-vista"></a>附录 A：如何在 Windows Vista 中的新硬件上安装内置的蓝牙驱动程序


本附录介绍了强制随 Windows Vista 上新的蓝牙无线安装蓝牙驱动程序的过程。 Windows XP SP2 使用类似的步骤，虽然一些详细信息各不相同。

## <a name="span-idstep1startdevicemanagerandselectthebluetoothradiospanspan-idstep1startdevicemanagerandselectthebluetoothradiospanspan-idstep1startdevicemanagerandselectthebluetoothradiospanstep-1-start-device-manager-and-select-the-bluetooth-radio"></a><span id="Step_1__Start_Device_Manager_and_Select_the_Bluetooth_Radio"></span><span id="step_1__start_device_manager_and_select_the_bluetooth_radio"></span><span id="STEP_1__START_DEVICE_MANAGER_AND_SELECT_THE_BLUETOOTH_RADIO"></span>步骤 1：启动设备管理器，然后选择蓝牙无线


若要启动设备管理器：

1.  单击**启动**，导航到**所有程序&gt;附件&gt;命令提示符下**，右键单击**命令提示符下**，然后单击**以管理员身份运行**以使用提升的权限打开命令窗口。
2.  键入以下内容：**Devmgmt.msc**

下**其他设备**，到蓝牙无线设备的设备管理器列表上的条目。 下图中，在广播的名称为"UGT"。 某些便携式计算机，您可能还需要第一个打开蓝牙无线使用如 Fn + F5 键组合。

![vista 蓝牙更新驱动程序软件](images/bthnewhwstep1.jpg)

若要验证所选的设备蓝牙无线，右键单击设备名称，然后依次**属性**以显示**属性**对话框。 上**详细信息**选项卡上，验证设备的蓝牙无线功能的兼容 ID:

USB\\Class\_e0&SubClass\_01&Prot\_01
### <a name="span-idstep2starttheupdatedriversoftwarewizardspanspan-idstep2starttheupdatedriversoftwarewizardspanspan-idstep2starttheupdatedriversoftwarewizardspanstep-2-start-the-update-driver-software-wizard"></a><span id="Step_2__Start_the_Update_Driver_Software_Wizard"></span><span id="step_2__start_the_update_driver_software_wizard"></span><span id="STEP_2__START_THE_UPDATE_DRIVER_SOFTWARE_WIZARD"></span>步骤 2：启动更新驱动程序软件向导

右键单击 Bluetooth 无线电节点，然后单击**更新驱动程序软件**。 若要转到下图中的页，单击**浏览计算机以查找驱动程序软件**。 若要手动选择的驱动程序，请单击**让我在我的计算机上从设备驱动程序的列表中选取**。

![vista 蓝牙更新驱动程序软件](images/bthnewhwstep2.jpg)

### <a name="span-idstep3selectthegenericbluetoothdriverspanspan-idstep3selectthegenericbluetoothdriverspanspan-idstep3selectthegenericbluetoothdriverspanstep-3-select-the-generic-bluetooth-driver"></a><span id="Step_3__Select_the_Generic_Bluetooth_Driver"></span><span id="step_3__select_the_generic_bluetooth_driver"></span><span id="STEP_3__SELECT_THE_GENERIC_BLUETOOTH_DRIVER"></span>步骤 3：选择泛型蓝牙驱动程序

更新驱动程序软件向导接下来显示可用的驱动程序的列表。 选择**Bluetooth 无线电收发器**，然后选择与您的系统，蓝牙无线下, 图中所示。 如果不确定使用哪个驱动程序，可用于测试的通用驱动程序。 若要执行此操作，请选择**泛型适配器**为制造商和**泛型 Bluetooth 适配器**作为模型。

![vista 蓝牙更新驱动程序软件](images/bthnewhwstep3.jpg)

选择驱动程序后，向导会要求您确认您想要在新的蓝牙无线上安装指定的驱动程序。 如果尝试在不蓝牙无线设备上安装蓝牙驱动程序，可能不会启动驱动程序。

如果正确加载该驱动程序，设备管理器应具有一个泛型 Bluetooth 适配器条目的 Bluetooth 无线电收发器节点下下, 图中所示。

![vista 蓝牙更新驱动程序软件](images/bthnewhwstep4.jpg)

如果该驱动程序启动失败，例如，如果 Windows 返回了一个启动错误代码，检查事件日志以帮助确定原因。

 

 





