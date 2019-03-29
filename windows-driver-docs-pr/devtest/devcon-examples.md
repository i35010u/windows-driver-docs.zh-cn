---
title: 设备控制台 (DevCon.exe) 示例
description: 设备控制台 (DevCon.exe) 示例
ms.assetid: 5af1e777-04ba-4e83-b239-f568a02a9460
keywords:
- DevCon WDK 示例
- 设备控制台 WDK 示例
- 示例 WDK DevCon
- DevCon WDK 命令
- 设备控制台 WDK 命令
- WDK DevCon 命令
- 示例 44 强制更新 HAL
- HAL 更新示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23508e68c050334b1090993d5b3b00921d9b4ed7
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350272"
---
# <a name="device-console-devconexe-examples"></a>设备控制台 (DevCon.exe) 示例


## <span id="ddk_devcon_examples_tools"></span><span id="DDK_DEVCON_EXAMPLES_TOOLS"></span>


本部分提供了以下设备控制台 (DevCon.exe) 命令的示例：

### <a name="span-iddevconhwidsspanspan-iddevconhwidsspandevcon-hwids"></a><span id="devcon_hwids"></span><span id="DEVCON_HWIDS"></span>DevCon HwIDs

[示例 1:查找所有硬件 Id](#ddk_example_1_find_all_hardware_ids_tools)

[示例 2:通过使用一种模式中找到硬件 Id](#ddk_example_2_find_hardware_ids_by_using_a_pattern_tools)

[示例 3:通过使用类找到硬件 Id](#ddk_example_3_find_hardware_ids_by_using_a_class_tools)

### <a name="span-iddevconclassesspanspan-iddevconclassesspandevcon-classes"></a><span id="devcon_classes"></span><span id="DEVCON_CLASSES"></span>DevCon 类

[示例 4:在本地计算机上的列表类](#ddk_example_4_list_classes_on_the_local_computer_tools)

[示例 5:在远程计算机上的列表类](#ddk_example_5_list_classes_on_the_remote_computer_tools)

### <a name="span-iddevconlistclassspanspan-iddevconlistclassspandevcon-listclass"></a><span id="devcon_listclass"></span><span id="DEVCON_LISTCLASS"></span>DevCon ListClass

[示例 6:设备安装程序类中的设备列表](#ddk_example_6_list_the_devices_in_a_device_setup_class_tools)

[示例 7:在远程计算机上的多个类的设备列表](#ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute)

### <a name="span-iddevcondriverfilesspanspan-iddevcondriverfilesspandevcon-driverfiles"></a><span id="devcon_driverfiles"></span><span id="DEVCON_DRIVERFILES"></span>DevCon DriverFiles

[示例 8:列出所有驱动程序文件](#ddk_example_8_list_all_driver_files_tools)

[示例 9:列出特定设备的驱动程序文件](#ddk_example_9_list_the_driver_files_of_a_particular_device_tools)

### <a name="span-iddevcondrivernodesspanspan-iddevcondrivernodesspandevcon-drivernodes"></a><span id="devcon_drivernodes"></span><span id="DEVCON_DRIVERNODES"></span>DevCon DriverNodes

[示例 10:列表由硬件 ID 模式的驱动程序包](#ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools)

[示例 11:通过设备实例 ID 模式列表驱动程序包](#ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool)

### <a name="span-iddevconresourcesspanspan-iddevconresourcesspandevcon-resources"></a><span id="devcon_resources"></span><span id="DEVCON_RESOURCES"></span>DevCon 资源

[示例 12:列出资源的类的设备](#ddk_example_12_list_resources_of_a_class_of_devices_tools)

[示例 13:列出资源的 ID 的远程计算机上的设备](#ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too)

### <a name="span-iddevconstackspanspan-iddevconstackspandevcon-stack"></a><span id="devcon_stack"></span><span id="DEVCON_STACK"></span>DevCon Stack

[示例 14:显示存储设备驱动程序堆栈](#ddk_example_14_display_the_driver_stack_for_storage_devices_tools)

[例如，如果希望：查找设备的安装程序类](#ddk_example_15_find_the_setup_class_of_a_device_tools)

[示例 16:在远程计算机上显示相关设备的堆栈](#ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu)

### <a name="span-iddevconstatusspanspan-iddevconstatusspandevcon-status"></a><span id="devcon_status"></span><span id="DEVCON_STATUS"></span>DevCon 状态

[示例 17:在本地计算机上显示的所有设备的状态](#ddk_example_17_display_the_status_of_all_devices_on_the_local_computer)

[18 的示例：显示设备通过设备实例 ID 的状态](#ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to)

[示例 19:在远程计算机上显示相关设备的状态](#ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu)

### <a name="span-iddevconfindspanspan-iddevconfindspandevcon-find"></a><span id="devcon_find"></span><span id="DEVCON_FIND"></span>DevCon 查找

[示例 20:查找设备硬件 ID 模式](#ddk_example_20_find_devices_by_hardware_id_pattern_tools)

[示例 21:查找设备通过设备实例 ID 或类](#ddk_example_21_find_devices_by_device_instance_id_or_class_tools)

### <a name="span-iddevconfindallspanspan-iddevconfindallspandevcon-findall"></a><span id="devcon_findall"></span><span id="DEVCON_FINDALL"></span>DevCon FindAll

[示例 22:查找 （并查找所有） 安装程序类中的设备](#ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools)

### <a name="span-iddevconclassfilterspanspan-iddevconclassfilterspandevcon-classfilter"></a><span id="devcon_classfilter"></span><span id="DEVCON_CLASSFILTER"></span>DevCon ClassFilter

[示例 23:显示安装程序类的筛选器驱动程序](#ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools)

[示例是 24:将筛选器驱动程序添加到安装程序类](#ddk_example_24_add_a_filter_driver_to_a_setup_class_tools)

[示例 25:类列表中插入筛选器驱动程序](#ddk_example_25_insert_a_filter_driver_in_the_class_list_tools)

[示例 26:替换为筛选器驱动程序](#ddk_example_26_replace_a_filter_driver_tools)

[示例 27:更改筛选器驱动程序的顺序](#ddk_example_27_change_the_order_of_filter_drivers_tools)

### <a name="span-iddevconenablespanspan-iddevconenablespandevcon-enable"></a><span id="devcon_enable"></span><span id="DEVCON_ENABLE"></span>DevCon 启用

[示例 28:启用特定设备](#ddk_example_28_enable_a_particular_device_tools)

[示例 29:使设备由类](#ddk_example_29_enable_devices_by_class_tools)

### <a name="span-iddevcondisablespanspan-iddevcondisablespandevcon-disable"></a><span id="devcon_disable"></span><span id="DEVCON_DISABLE"></span>DevCon 禁用

[示例 30:通过 ID 模式来禁用设备](#ddk_example_30_disable_devices_by_an_id_pattern_tools)

[示例 31:禁用设备通过设备实例 ID](#ddk_example_31_disable_devices_by_device_instance_id_tools)

### <a name="span-iddevconupdateandupdatenispanspan-iddevconupdateandupdatenispandevcon-update-and-updateni"></a><span id="devcon_update_and_updateni"></span><span id="DEVCON_UPDATE_AND_UPDATENI"></span>DevCon 更新和 UpdateNI

[示例 32:通信端口的驱动程序更新](#ddk_example_32_update_the_driver_for_communication_ports_tools)

[示例 44:强制更新 HAL](#ddk_example_44_forcibly_update_the_hal_tools)

### <a name="span-iddevconinstallspanspan-iddevconinstallspandevcon-install"></a><span id="devcon_install"></span><span id="DEVCON_INSTALL"></span>DevCon 安装

[示例 33:安装设备](#ddk_example_33_install_a_device_tools)

[示例 34:安装使用无人参与的安装的设备](#ddk_example_34_install_a_device_using_unattended_setup_tools)

### <a name="span-iddevconremovespanspan-iddevconremovespandevcon-remove"></a><span id="devcon_remove"></span><span id="DEVCON_REMOVE"></span>DevCon 删除

[示例 35:通过设备实例 ID 模式中删除的设备](#ddk_example_35_remove_devices_by_device_instance_id_pattern_tools)

[示例 36:删除特定网络设备](#ddk_example_36_remove_a_particular_network_device_tools)

### <a name="span-iddevconrescanspanspan-iddevconrescanspandevcon-rescan"></a><span id="devcon_rescan"></span><span id="DEVCON_RESCAN"></span>DevCon 重新扫描

[示例 37:扫描计算机以查找新设备](#ddk_example_37_scan_the_computer_for_new_devices_tools)

### <a name="span-iddevconrestartspanspan-iddevconrestartspandevcon-restart"></a><span id="devcon_restart"></span><span id="DEVCON_RESTART"></span>DevCon 重新启动

[示例 38:重启设备](#ddk_example_38_restart_a_device_tools)

### <a name="span-iddevconstatus2spanspan-iddevconstatus2spandevcon-status"></a><span id="devcon_status2"></span><span id="DEVCON_STATUS2"></span>DevCon 状态

[示例 39:重新启动本地计算机](#ddk_example_39_reboot_the_local_computer_tools)

### <a name="span-iddevconsethwidspanspan-iddevconsethwidspandevcon-sethwid"></a><span id="devcon_sethwid"></span><span id="DEVCON_SETHWID"></span>DevCon SetHwID

[示例 40:将硬件 ID 分配给旧的设备](#ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools)

[示例 41:添加到远程计算机上的所有旧设备的硬件 ID](#ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com)

[示例 42:从远程计算机上的所有旧设备中删除硬件 ID](#ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot)

[示例 43:添加、 删除和替换的硬件 Id](#ddk_example_43_add_delete_and_replace_hardwareids_tools)

[示例 44:强制更新 HAL](#ddk_example_44_forcibly_update_the_hal_tools)

### <a name="span-iddevcondpadddpdeleteddpenumspanspan-iddevcondpadddpdeleteddpenumspandevcon-dpadd-dpdeleted-dpenum"></a><span id="devcon_dp_add__dp_deleted__dp_enum"></span><span id="DEVCON_DP_ADD__DP_DELETED__DP_ENUM"></span>DevCon dp\_添加，dp\_删除 dp\_枚举

[示例 45:添加和删除驱动程序包](example-45--add-and-remove-driver-packages.md)

### <span id="ddk_example_1_find_all_hardware_ids_tools"></span><span id="DDK_EXAMPLE_1_FIND_ALL_HARDWARE_IDS_TOOLS"></span><a name="ddk_example_1_find_all_hardware_ids_tools"></a>示例 1:查找所有硬件 Id

由于 DevCon 操作使用 Id 和 ID 模式，首先标识设备，一种常见步骤使用 DevCon 是在计算机上创建的设备硬件 ID 引用文件。

下面的命令使用[ **DevCon HwIDs** ](devcon-hwids.md)操作，返回 Id 和设备说明。 它使用通配符 (* *\\* * *) 来表示本地计算机上的所有设备。

```
devcon hwids *
```

由于输出是长时间和已用重复，将输出保存在文本文件供参考。

下面的命令使用通配符 (**\\* * *) 来表示计算机上的所有设备。它使用的重定向字符 (*<em>&gt;</em>*) 将命令输出保存在 hwids.txt 文件中。

```
devcon hwids * > hwids.txt
```

以下命令查找远程计算机 Server01 上的硬件设备的 Id。 它使用 **/m**参数来指定远程计算机的名称。 该命令将输出重定向到 server01\_hwids.txt 文件以供日后参考。

**请注意**  此命令会失败，除非用户在远程计算机上具有所需的权限。 若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和 Windows 7 的计算机上，组策略默认情况下禁用远程访问服务。 运行 Windows Driver Kit (WDK) 8.1 和 Windows Driver Kit (WDK) 8 的计算机上，远程访问将不可用。

 

```
devcon /m:\\server01 hwids * > server01_hwids.txt
```

### <span id="ddk_example_2_find_hardware_ids_by_using_a_pattern_tools"></span><span id="DDK_EXAMPLE_2_FIND_HARDWARE_IDS_BY_USING_A_PATTERN_TOOLS"></span><a name="ddk_example_2_find_hardware_ids_by_using_a_pattern_tools"></a>示例 2:通过使用一种模式中找到硬件 Id

若要查找的硬件特定设备的 Id，输入硬件 ID 或模式、 兼容 ID 或模式，设备实例 ID 或模式或设备安装程序类的名称。

下面的命令使用**DevCon HwIDs**操作和模式，若要查找的硬件 Id 的软盘驱动器的计算机上。 （用户假设模式显示在一个设备的标识符。）该命令使用通配符 (* *\\* * *) 来表示可能的前面或后面的单词"软"在任何 Id 的所有字符。

```
devcon hwids *floppy*
```

在响应中，DevCon 显示计算机上的设备实例 ID、 硬件 ID 和兼容 ID 的软盘驱动器。 在后续 DevCon 命令中，可以使用这些 Id。

```
FDC\GENERIC_FLOPPY_DRIVE\5&39194F6D&0&0
    Name: Floppy disk drive
    Hardware ID's:
        FDC\GENERIC_FLOPPY_DRIVE
    Compatible ID's:
        GenFloppyDisk
1 matching device(s) found.
```

在这种情况下，短语"floppy"硬件 ID 或兼容的计算机上只有一个设备 ID 中发生。 如果它出现在多个设备的 ID，使用"floppy"及其 Id 中的所有设备将都出现在输出中。

### <span id="ddk_example_3_find_hardware_ids_by_using_a_class_tools"></span><span id="DDK_EXAMPLE_3_FIND_HARDWARE_IDS_BY_USING_A_CLASS_TOOLS"></span><a name="ddk_example_3_find_hardware_ids_by_using_a_class_tools"></a>示例 3:通过使用类找到硬件 Id

下面的命令使用[ **DevCon HwIDs** ](devcon-hwids.md)操作和设备安装程序类，以在端口设备安装程序类中找到的硬件 Id 的所有设备。 等号 (**=**) 在类名前面指示它是一个类，不是 id。

```
devcon hwids =ports
```

在响应中，DevCon 显示硬件 Id 和兼容的端口安装程序类中的三个设备的 Id。

```
ACPI\PNP0401\4&B4063F4&0
    Name: ECP Printer Port (LPT1)
    Hardware ID's:
        ACPI\PNP0401
        *PNP0401
ACPI\PNP0501\1
    Name: Communications Port (COM1)
    Hardware ID's:
        ACPI\PNP0501
        *PNP0501
ACPI\PNP0501\2
    Name: Communications Port (COM2)
    Hardware ID's:
        ACPI\PNP0501
        *PNP0501
3 matching device(s) found.
```

### <span id="ddk_example_4_list_classes_on_the_local_computer_tools"></span><span id="DDK_EXAMPLE_4_LIST_CLASSES_ON_THE_LOCAL_COMPUTER_TOOLS"></span><a name="ddk_example_4_list_classes_on_the_local_computer_tools"></a>示例 4:在本地计算机上的列表类

DevCon 操作可以使用设备安装程序类来标识设备，因为它可用于在计算机上创建的设备的设备安装程序类的引用文件。

下面的命令使用[ **DevCon 类**](devcon-classes.md)操作，返回的列表和说明的所有类的计算机。

```
devcon classes
```

由于输出是长时间和已用重复，将输出保存在文本文件供参考。

下面的命令的计算机上显示所有的设备类别。 它使用的重定向字符 (**&gt;**) 将命令输出保存在 classes.txt 文件中。

```
devcon classes > classes.txt
```

### <span id="ddk_example_5_list_classes_on_the_remote_computer_tools"></span><span id="DDK_EXAMPLE_5_LIST_CLASSES_ON_THE_REMOTE_COMPUTER_TOOLS"></span><a name="ddk_example_5_list_classes_on_the_remote_computer_tools"></a>示例 5:在远程计算机上的列表类

下面的命令使用[ **DevCon 类**](devcon-classes.md)操作可列出在远程计算机 Server01 上的设备安装程序类：

```
devcon /m:\\server01 classes
```

由于输出是长时间和已用重复，将输出保存在文本文件供参考。

下面的命令使用重定向字符 (**&gt;**) 以将命令输出保存在 server01\_classes.txt 文件。

```
devcon /m:\\server01 classes > server01_classes.txt
```

### <span id="ddk_example_6_list_the_devices_in_a_device_setup_class_tools"></span><span id="DDK_EXAMPLE_6_LIST_THE_DEVICES_IN_A_DEVICE_SETUP_CLASS_TOOLS"></span><a name="ddk_example_6_list_the_devices_in_a_device_setup_class_tools"></a>示例 6:设备安装程序类中的设备列表

下面的命令使用[ **DevCon ListClass** ](devcon-listclass.md)操作可列出 Net，网络适配器的设备安装程序类中的设备。

```
devcon listclass net
```

在响应中，DevCon 显示设备实例 ID 和每个设备的网络安装程序类中的说明。

```
Listing 6 device(s) for setup class "Net" (Network adapters).
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0: 3Com 3C920 Integrated Fast Ethernet Controller (3C905C-TX Compatible)
ROOT\MS_L2TPMINIPORT\0000                                   : WAN Miniport (L2TP)
ROOT\MS_NDISWANIP\0000                                      : WAN Miniport (IP)
ROOT\MS_PPPOEMINIPORT\0000                                  : WAN Miniport (PPPOE)
ROOT\MS_PPTPMINIPORT\0000                                   : WAN Miniport (PPTP)
ROOT\MS_PTIMINIPORT\0000                                    : Direct Parallel
```

此显示中，虽然令人感兴趣，但不提供硬件的净安装程序类中的设备的 Id。 下面的命令使用[ **DevCon HwIDs** ](devcon-hwids.md)操作可列出的净安装程序类中的设备。 在中**DevCon HwIDs**命令时，类名前面有一个等号 (**=**) 以指示它是一个类，不是 id。

```
devcon hwids =net
```

生成的显示列出 Net 类中的设备，并在类中包含设备实例 ID、 硬件 Id 和兼容 Id 的设备。

```
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0
    Name: 3Com 3C920 Integrated Fast Ethernet Controller (3C905C-TX Compatible)
    Hardware ID's:
        PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78
        PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028
        PCI\VEN_10B7&DEV_9200&CC_020000
        PCI\VEN_10B7&DEV_9200&CC_0200
    Compatible ID's:
        PCI\VEN_10B7&DEV_9200&REV_78
        PCI\VEN_10B7&DEV_9200
        PCI\VEN_10B7&CC_020000
        PCI\VEN_10B7&CC_0200
 PCI\VEN_10B7
        PCI\CC_020000
 PCI\CC_0200
ROOT\MS_L2TPMINIPORT\0000
    Name: WAN Miniport (L2TP)
    Hardware ID's:
        ms_l2tpminiport
ROOT\MS_NDISWANIP\0000
    Name: WAN Miniport (IP)
    Hardware ID's:
        ms_ndiswanip
ROOT\MS_PPPOEMINIPORT\0000
    Name: WAN Miniport (PPPOE)
    Hardware ID's:
        ms_pppoeminiport
ROOT\MS_PPTPMINIPORT\0000
    Name: WAN Miniport (PPTP)
    Hardware ID's:
        ms_pptpminiport
ROOT\MS_PTIMINIPORT\0000
    Name: Direct Parallel
    Hardware ID's:
        ms_ptiminiport
6 matching device(s) found.
```

### <span id="ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute"></span><span id="DDK_EXAMPLE_7_LIST_THE_DEVICES_IN_MULTIPLE_CLASSES_ON_A_REMOTE_COMPUTE"></span><a name="ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute"></a>示例 7:在远程计算机上的多个类的设备列表

下面的命令使用[ **DevCon ListClass** ](devcon-listclass.md)操作可列出的设备中的磁盘驱动器、 CDROM 和 TapeDrive 类上 Server01 远程计算机。

```
devcon /m:\\server01 listclass diskdrive cdrom tapedrive
```

在响应中，DevCon 远程计算机上显示这些类中的设备。

```
Listing 1 device(s) for setup class "DiskDrive" (Disk drives) on \\server01.
IDE\DISKWDC_WD204BA_____________________________16.13M16\4457572D414D3730323136333938203120202020: WDC WD204BA
Listing 1 device(s) for setup class "CDROM" (DVD/CD-ROM drives) on \\server01.
IDE\CDROMSAMSUNG_DVD-ROM_SD-608__________________2.2_____\4&13B4AFD&0&0.0.0: SAMSUNG DVD-ROM SD-608
No devices for setup class "TapeDrive" (Tape drives) on \\server01.
```

### <span id="ddk_example_8_list_all_driver_files_tools"></span><span id="DDK_EXAMPLE_8_LIST_ALL_DRIVER_FILES_TOOLS"></span><a name="ddk_example_8_list_all_driver_files_tools"></a>示例 8:列出所有驱动程序文件

下面的命令使用[ **DevCon DriverFiles** ](devcon-driverfiles.md)操作可列出系统上的设备使用的驱动程序的文件名称。 该命令使用通配符 (**\\* * *) 以指示系统上的所有设备。由于输出是广泛的该命令使用重定向字符 (*<em>&gt;</em>*) 将输出重定向到参考文件中，driverfiles.txt。

```
devcon driverfiles * > driverfiles.txt
```

### <span id="ddk_example_9_list_the_driver_files_of_a_particular_device_tools"></span><span id="DDK_EXAMPLE_9_LIST_THE_DRIVER_FILES_OF_A_PARTICULAR_DEVICE_TOOLS"></span><a name="ddk_example_9_list_the_driver_files_of_a_particular_device_tools"></a>示例 9:列出特定设备的驱动程序文件

下面的命令使用[ **DevCon DriverFiles** ](devcon-driverfiles.md)操作要搜索在本地计算机上的鼠标设备使用的设备驱动程序。 将设备标识由一个其硬件 Id，HID\\Vid\_045e & Pid\_0039 & Rev\_0121年。 硬件 ID 括在引号中，因为它包括 & 号字符 (**&**)。

```
devcon driverfiles "HID\Vid_045e&Pid_0039&Rev_0121"
```

在响应中，DevCon 显示支持的鼠标设备的两个设备驱动程序。

```
HID\VID_045E&PID_0039\6&DC36FDE&0&0000
    Name: Microsoft USB IntelliMouse Optical
    Driver installed from c:\windows\inf\msmouse.inf [HID_Mouse_Inst]. 2 file(s)
 used by driver:
        C:\WINDOWS\System32\DRIVERS\mouhid.sys
        C:\WINDOWS\System32\DRIVERS\mouclass.sys
1 matching device(s) found.
```

### <span id="ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools"></span><span id="DDK_EXAMPLE_10_LIST_DRIVER_PACKAGES_BY_HARDWARE_ID_PATTERN_TOOLS"></span><a name="ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools"></a>示例 10:列表由硬件 ID 模式的驱动程序包

下面的命令使用[ **DevCon DriverNodes** ](devcon-drivernodes.md)命令和一个 ID 模式列出软件枚举设备的驱动程序节点。 模式可用于查找有关可能不在相同的安装程序类的相似设备的信息。

下面的命令使用 ID 模式**sw\\*** 来指定在其硬件 Id 或兼容 Id 开始使用"软件"，即，软件枚举设备的设备。

```
devcon drivernodes sw*
```

在响应中，DevCon 显示系统上的软件枚举设备的驱动程序节点。

```
SW\{A7C7A5B0-5AF3-11D1-9CED-00A024BF0407}\{9B365890-165F-11D0-A195-0020AFD156E4}

 Name: Microsoft Kernel System Audio Device
DriverNode #0:
    Inf file is c:\windows\inf\wdmaudio.inf
    Inf section is WDM_SYSAUDIO
    Driver description is Microsoft Kernel System Audio Device
    Manufacturer name is Microsoft
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002244
        Inf is digitally signed
SW\{B7EAFDC0-A680-11D0-96D8-00AA0051E51D}\{9B365890-165F-11D0-A195-0020AFD156E4}

    Name: Microsoft Kernel Wave Audio Mixer
DriverNode #0:
    Inf file is c:\windows\inf\wdmaudio.inf
    Inf section is WDM_KMIXER
    Driver description is Microsoft Kernel Wave Audio Mixer
    Manufacturer name is Microsoft
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002244
        Inf is digitally signed
SW\{CD171DE3-69E5-11D2-B56D-0000F8754380}\{9B365890-165F-11D0-A195-0020AFD156E4}

    Name: Microsoft WINMM WDM Audio Compatibility Driver
DriverNode #0:
    Inf file is c:\windows\inf\wdmaudio.inf
    Inf section is WDM_WDMAUD
    Driver description is Microsoft WINMM WDM Audio Compatibility Driver
    Manufacturer name is Microsoft
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002244
        Inf is digitally signed
3 matching device(s) found.
```

### <span id="ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool"></span><span id="DDK_EXAMPLE_11_LIST_DRIVER_PACKAGES_BY_DEVICE_INSTANCE_ID_PATTERN_TOOL"></span><a name="ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool"></a>示例 11:通过设备实例 ID 模式列表驱动程序包

下面的命令使用[ **DevCon DriverNodes** ](devcon-drivernodes.md)操作可列出其设备实例 Id 的所有设备的驱动程序包以根开头\\媒体，即，在枚举中的设备\\根\\媒体注册表子项。 该命令使用在字符 (**@**) 以指示该短语中设备实例 id。

```
devcon drivernodes @ROOT\MEDIA*
```

在响应中，DevCon 显示其设备实例 ID 开头的设备的驱动程序节点"根\\媒体。"

```
ROOT\MEDIA\MS_MMACM
    Name: Audio Codecs
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMACM
    Driver description is Audio Codecs
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
ROOT\MEDIA\MS_MMDRV
    Name: Legacy Audio Drivers
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMDRV
    Driver description is Legacy Audio Drivers
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
ROOT\MEDIA\MS_MMMCI
    Name: Media Control Devices
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMMCI
    Driver description is Media Control Devices
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
ROOT\MEDIA\MS_MMVCD
    Name: Legacy Video Capture Devices
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMVCD
    Driver description is Legacy Video Capture Devices
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
ROOT\MEDIA\MS_MMVID
    Name: Video Codecs
DriverNode #0:
    Inf file is c:\windows\inf\wave.inf
    Inf section is MS_MMVID
    Driver description is Video Codecs
    Manufacturer name is (Standard system devices)
    Provider name is Microsoft
    Driver date is 7/1/2001
    Driver version is 5.1.2535.0
    Driver node rank is 0
    Driver node flags are 00002240
        Inf is digitally signed
5 matching device(s) found.
```

### <span id="ddk_example_12_list_resources_of_a_class_of_devices_tools"></span><span id="DDK_EXAMPLE_12_LIST_RESOURCES_OF_A_CLASS_OF_DEVICES_TOOLS"></span><a name="ddk_example_12_list_resources_of_a_class_of_devices_tools"></a>示例 12:列出资源的类的设备

下面的命令使用[ **DevCon 资源**](devcon-resources.md)操作来显示分配给 Hdc 设备安装程序类中的设备的资源。 此类包括 IDE 控制器。 等号 (**=**) 添加到"hdc"以指示它是一个类，而不是 id。

```
devcon resources =hdc
```

在响应中，DevCon 列出分配给本地计算机上的 IDE 控制器的资源。

```
PCI\VEN_8086&DEV_244B&SUBSYS_00000000&REV_02\3&29E81982&0&F9
    Name: Intel(r) 82801BA Bus Master IDE Controller
    Device is currently using the following resources:
        IO  : ffa0-ffaf
PCIIDE\IDECHANNEL\4&37E53584&0&0
    Name: Primary IDE Channel
    Device is currently using the following resources:
        IO  : 01f0-01f7
        IO  : 03f6-03f6
        IRQ : 14
PCIIDE\IDECHANNEL\4&37E53584&0&1
    Name: Secondary IDE Channel
    Device is currently using the following resources:
        IO  : 0170-0177
        IO  : 0376-0376
        IRQ : 15
3 matching device(s) found.
```

### <span id="ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too"></span><span id="DDK_EXAMPLE_13_LIST_RESOURCES_OF_DEVICE_ON_A_REMOTE_COMPUTER_BY_ID_TOO"></span><a name="ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too"></a>示例 13:列出资源的 ID 的远程计算机上的设备

下面的命令使用[ **DevCon 资源**](devcon-resources.md)操作以列出的资源分配给系统计时器在 Server01 远程计算机。 该命令使用的系统计时器，ACPI 的硬件 ID\\PNP0100，来指定的设备。

```
devcon /m:\\Server01 resources *PNP0100
```

在响应中，DevCon 显示 Server01 系统计时器的资源。

```
ROOT\*PNP0100\PNPBIOS_8
    Name: System timer
    Device has the following resources reserved:
        IO  : 0040-005f
        IRQ : 0
1 matching device(s) found on \\server01.
```

以下命令使用 DevCon 资源命令中的远程系统计时器的设备实例 ID。 在字符 (**@**) 指示的字符串是一个设备实例 ID、 不硬件 ID 或兼容 id。

```
devcon /m:\\Server01 resources @ACPI\PNP0100\4&b4063f4&0
```

### <span id="ddk_example_14_display_the_driver_stack_for_storage_devices_tools"></span><span id="DDK_EXAMPLE_14_DISPLAY_THE_DRIVER_STACK_FOR_STORAGE_DEVICES_TOOLS"></span><a name="ddk_example_14_display_the_driver_stack_for_storage_devices_tools"></a>示例 14:显示存储设备驱动程序堆栈

下面的命令使用[ **DevCon 堆栈**](devcon-stack.md)操作来搜索该卷中的设备安装程序类，并显示这些设备的预期的驱动程序堆栈。 等号 (**=**) 指示字符串为类名。

```
devcon stack =Volume
```

在响应中，DevCon 显示卷类中的设备的预期的堆栈。 返回的数据包括设备实例 ID 和说明的每个设备的 GUID 和设备安装程序类的名称、 上限和下限的筛选器驱动程序和控制服务的名称 （如果有）。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE32323533OFFSET271167600LENGTH6E00D0C00
    Name: Generic volume
    Setup Class: {71A27CDD-812A-11D0-BEC7-08002BE2092F} Volume
    Class upper filters:
        VolSnap
    Controlling service:
        (none)
STORAGE\VOLUME\1&30A96598&0&SIGNATURE32323533OFFSET7E00LENGTH27115F800
    Name: Generic volume
    Setup Class: {71A27CDD-812A-11D0-BEC7-08002BE2092F} Volume
    Class upper filters:
        VolSnap
    Controlling service:
        (none)
2 matching device(s) found.
```

### <span id="ddk_example_15_find_the_setup_class_of_a_device_tools"></span><span id="DDK_EXAMPLE_15_FIND_THE_SETUP_CLASS_OF_A_DEVICE_TOOLS"></span><a name="ddk_example_15_find_the_setup_class_of_a_device_tools"></a>例如，如果希望：查找设备的安装程序类

[ **DevCon 堆栈**](devcon-stack.md)操作返回设备包括上限和下限的筛选器驱动程序的安装程序类。 以下命令查找通过查找其设备实例 ID，然后使用设备实例 ID 来查找其安装程序类的打印机端口接口的安装程序类。

下面的命令使用[ **DevCon HwIDs** ](devcon-hwids.md)操作以查找设备实例 ID 的打印机端口接口通过使用"LPT，"短语中打印机端口硬件 id。

```
devcon hwids *lpt*
```

在响应中，DevCon 返回 （显示为粗体文本显示） 的设备实例 ID 和打印机端口接口的硬件 ID。

```
LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1
    Name: Printer Port Logical Interface
    Hardware ID's:
        LPTENUM\MicrosoftRawPort958A
        MicrosoftRawPort958A
1 matching device(s) found.
```

下一个命令使用[ **DevCon 堆栈**](devcon-stack.md)操作以查找设备实例 id。 所表示的设备的设备安装程序类 在字符 (**@**) 标识的 ID 作为设备实例 id。 ID 被用引号引起来，因为它包含 & 字符。

```
devcon stack "@LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1"
```

在响应中，DevCon 显示打印机端口界面，包括类的驱动程序堆栈。 显示就会发现打印机端口是系统类中。

```
LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1
    Name: Printer Port Logical Interface
    Setup Class: {4D36E97D-E325-11CE-BFC1-08002BE10318} System
    Controlling service:
        (none)
1 matching device(s) found.
```

### <span id="ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu"></span><span id="DDK_EXAMPLE_16_DISPLAY_THE_STACK_FOR_RELATED_DEVICES_ON_A_REMOTE_COMPU"></span><a name="ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu"></a>示例 16:在远程计算机上显示相关设备的堆栈

下面的命令使用**DevCon 堆栈**操作来显示预期堆栈微型端口驱动程序上的设备 Server01 远程计算机。 它具有"微型端口"的设备的网络安装程序类中的搜索中其硬件 ID 或兼容 id。

请注意，此命令首先将搜索限定为 Net 的安装程序类，然后查找"微型端口"的字符串。 找不到以外的净安装程序类中的设备。

```
devcon /m:\\server01 stack =net *miniport*
```

在响应中，DevCon Server01 上显示微型端口驱动程序的预期的的堆栈。

```
ROOT\MS_L2TPMINIPORT\0000
    Name: WAN Miniport (L2TP)
    Setup Class: {4D36E972-E325-11CE-BFC1-08002BE10318} Net
    Controlling service:
        Rasl2tp
ROOT\MS_PPPOEMINIPORT\0000
    Name: WAN Miniport (PPPOE)
    Setup Class: {4D36E972-E325-11CE-BFC1-08002BE10318} Net
    Controlling service:
        RasPppoe
    Lower filters:
        NdisTapi
ROOT\MS_PPTPMINIPORT\0000
    Name: WAN Miniport (PPTP)
    Setup Class: {4D36E972-E325-11CE-BFC1-08002BE10318} Net
    Controlling service:
        PptpMiniport
    Lower filters:
        NdisTapi
ROOT\MS_PTIMINIPORT\0000
    Name: Direct Parallel
    Setup Class: {4D36E972-E325-11CE-BFC1-08002BE10318} Net
    Controlling service:
        Raspti
    Lower filters:
        PtiLink
4 matching device(s) found on \\Server01.
```

### <span id="ddk_example_17_display_the_status_of_all_devices_on_the_local_computer"></span><span id="DDK_EXAMPLE_17_DISPLAY_THE_STATUS_OF_ALL_DEVICES_ON_THE_LOCAL_COMPUTER"></span><a name="ddk_example_17_display_the_status_of_all_devices_on_the_local_computer"></a>示例 17:在本地计算机上显示的所有设备的状态

下面的命令使用[ **DevCon 状态**](devcon-status.md)操作以在本地计算机上找到的所有设备的状态。 它然后将状态保存在 status.txt 文件日志记录或更高版本中查看。 该命令使用通配符 (**\\* * *) 来表示所有设备和重定向字符 (*<em>&gt;</em>*) 将输出重定向到 status.txt 文件。

```
devcon status * > status.txt
```

### <span id="ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to"></span><span id="DDK_EXAMPLE_18_DISPLAY_THE_STATUS_OF_A_DEVICE_BY_DEVICE_INSTANCE_ID_TO"></span><a name="ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to"></a>18 的示例：显示设备通过设备实例 ID 的状态

找不到特定设备的状态的最可靠方法是使用设备的设备实例 ID。

下面的命令在本地计算机上使用的设备实例 ID 的 I/O 控制器[ **DevCon 状态**](devcon-status.md)命令。 该命令包含设备实例 ID 的设备，PCI\\也执行\_8086 & 开发\_1130年 & SUBSYS\_00000000 和修订号\_02\\3 29E81982 0 & 00。 在字符 (**@**) 作为前缀 ID 标识的字符串作为设备实例 id。 ID 必须括在引号中，因为它包括 & 字符。

```
devcon status "@PCI\VEN_8086&DEV_1130&SUBSYS_00000000&REV_02\3&29E81982&0&00"
```

在响应中，DevCon 显示 I/O 控制器的状态。

```
PCI\VEN_8086&DEV_1130&SUBSYS_00000000&REV_02\3&29E81982&0&00
    Name: Intel(R) 82815 Processor to I/O Controller - 1130
    Driver is running.
1 matching device(s) found.
```

### <span id="ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu"></span><span id="DDK_EXAMPLE_19_DISPLAY_THE_STATUS_OF_RELATED_DEVICES_ON_A_REMOTE_COMPU"></span><a name="ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu"></a>示例 19:在远程计算机上显示相关设备的状态

下面的命令使用[ **DevCon 状态**](devcon-status.md)操作以在 Server01 远程计算机上显示的与存储相关的特定设备的状态。 它会搜索以下设备：

-   磁盘驱动器 GenDisk

-   CD-ROM 驱动器 GenCdRom

-   软盘驱动器、 FDC\\泛型\_软盘\_驱动器

-   卷、 存储\\卷

-   逻辑磁盘管理器中，根\\DMIO

-   卷管理器中，根\\FTDISK

-   软盘控制器，ACPI\\PNP0700

在命令中，每个 ID 与其他人由空格分隔开来。 请注意，GenDisk 和 GenCdRom 兼容 Id，而其他 Id 是硬件 Id。

```
devcon /m:\\server01 status GenDisk GenCdRom FDC\GENERIC_FLOPPY_DRIVE STORAGE\Volume ROOT\DMIO ROOT\FTDISK ACPI\PNP0700
```

在响应中，DevCon 显示每个设备的状态。

```
FDC\GENERIC_FLOPPY_DRIVE\1&3A2146F1&0&0
    Name: Floppy disk drive
    Driver is running.
IDE\CDROMSAMSUNG_DVD-ROM_SD-608__________________2.2_____\4&13B4AFD&0&0.0.0
    Name: SAMSUNG DVD-ROM SD-608
    Driver is running.
IDE\DISKWDC_WD204BA_____________________________16.13M16\4457572D414D373032313633393820312
0202020
    Name: WDC WD204BA
    Driver is running.
ROOT\DMIO\0000
    Name: Logical Disk Manager
    Driver is running.
ROOT\FLOPPYDISK\0000
    Device has a problem: 28.
ROOT\FLOPPYDISK\0002
    Device has a problem: 01.
ROOT\FLOPPYDISK\0003
    Device has a problem: 01.
ROOT\FLOPPYDISK\0004
    Device is currently stopped.
ROOT\FTDISK\0000
    Name: Volume Manager
    Driver is running.
STORAGE\VOLUME\1&30A96598&0&SIGNATUREEA1AA9C7OFFSET1770DF800LENGTH3494AEA00
    Name: Generic volume
    Driver is running.
STORAGE\VOLUME\1&30A96598&0&SIGNATUREEA1AA9C7OFFSET7E00LENGTH1770CFC00
    Name: Generic volume
    Driver is running.
11 matching device(s) found on \\Server01.
```

### <span id="ddk_example_20_find_devices_by_hardware_id_pattern_tools"></span><span id="DDK_EXAMPLE_20_FIND_DEVICES_BY_HARDWARE_ID_PATTERN_TOOLS"></span><a name="ddk_example_20_find_devices_by_hardware_id_pattern_tools"></a>示例 20:查找设备硬件 ID 模式

下面的命令使用[ **DevCon 查找**](devcon-find.md)操作以搜索远程计算机 Server01 上的鼠标设备。 具体而言，此命令会搜索在 Server01 计算机的设备的硬件 ID 或兼容 ID 包括"mou。"

```
devcon /m:\\Server01 find *mou*
```

在这种情况下，DevCon 找到这两种两个鼠标设备。

```
ROOT\*PNP0F03\1_0_21_0_31_0                                 : Microsoft PS/2 Mouse
ROOT\RDP_MOU\0000                                           : Terminal Server Mouse Driver
```

因为所有 DevCon 显示操作还会都找到硬件 Id，可以使用任何显示操作要搜索的硬件 Id。 选择所需的输出中的内容的操作。 例如，若要在本地计算机上使用查找设备驱动程序的与鼠标相关的设备，提交以下命令。

```
devcon driverfiles *mou*
```

在响应中，DevCon 查找设备，并列出其驱动程序。

```
HID\VID_045E&PID_0039\6&DC36FDE&0&0000
    Name: Microsoft USB IntelliMouse Optical
    Driver installed from c:\windows\inf\msmouse.inf [HID_Mouse_Inst]. 2 file(s) used by d
river:
        C:\WINDOWS\System32\DRIVERS\mouhid.sys
        C:\WINDOWS\System32\DRIVERS\mouclass.sys
ROOT\RDP_MOU\0000
    Name: Terminal Server Mouse Driver
    Driver installed from c:\windows\inf\machine.inf [RDP_MOU]. 2 file(s) used by driver:
        C:\WINDOWS\System32\DRIVERS\termdd.sys
        C:\WINDOWS\System32\DRIVERS\mouclass.sys
2 matching device(s) found.
```

### <span id="ddk_example_21_find_devices_by_device_instance_id_or_class_tools"></span><span id="DDK_EXAMPLE_21_FIND_DEVICES_BY_DEVICE_INSTANCE_ID_OR_CLASS_TOOLS"></span><a name="ddk_example_21_find_devices_by_device_instance_id_or_class_tools"></a>示例 21:查找设备通过设备实例 ID 或类

以下命令使用[ **DevCon 查找**](devcon-find.md)操作来显示本地计算机上的所有旧设备。 由于旧设备不具有硬件 ID，必须搜索它们按其设备实例 ID （注册表路径），根\\旧式或其安装程序类，LegacyDriver。

第一个命令的设备实例 ID 模式来查找旧驱动程序。 ID 模式以开头字符处 (**@**) 以指示设备实例 ID 和通配符字符 (* *\\* * *) 的根目录中查找所有设备\\旧版子项。

```
devcon find @root\legacy*
```

第二个命令通过搜索 LegacyDriver 类中的所有设备查找旧设备。

```
devcon find =legacydriver
```

这两个命令生成相同的输出，在这种情况下，查找相同的 27 旧设备。

```
ROOT\LEGACY_AFD\0000                                        : AFD Networking Support Environment
ROOT\LEGACY_BEEP\0000                                       : Beep
ROOT\LEGACY_DMBOOT\0000                                     : dmboot
ROOT\LEGACY_DMLOAD\0000                                     : dmload
ROOT\LEGACY_FIPS\0000                                       : Fips
ROOT\LEGACY_GPC\0000                                        : Generic Packet Classifier
ROOT\LEGACY_IPSEC\0000                                      : ipsec
ROOT\LEGACY_KSECDD\0000                                     : ksecdd
ROOT\LEGACY_MNMDD\0000                                      : mnmdd
ROOT\LEGACY_MOUNTMGR\0000                                   : mountmgr
ROOT\LEGACY_NDIS\0000                                       : ndis
ROOT\LEGACY_NDISTAPI\0000                                   : Remote Access NDIS TAPI Driver
ROOT\LEGACY_NDISUIO\0000                                    : NDIS Usermode I/O Protocol
ROOT\LEGACY_NDPROXY\0000                                    : NDProxy
ROOT\LEGACY_NETBT\0000                                      : netbt
ROOT\LEGACY_NULL\0000                                       : Null
ROOT\LEGACY_PARTMGR\0000                                    : PartMgr
ROOT\LEGACY_PARVDM\0000                                     : ParVdm
ROOT\LEGACY_RASACD\0000                                     : Remote Access Auto Connection Driver
ROOT\LEGACY_RDPCDD\0000                                     : RDPCDD
ROOT\LEGACY_RDPWD\0000                                      : RDPWD
ROOT\LEGACY_TCPIP\0000                                      : tcpip
ROOT\LEGACY_TDPIPE\0000                                     : TDPIPE
ROOT\LEGACY_TDTCP\0000                                      : TDTCP
ROOT\LEGACY_VGASAVE\0000                                    : VgaSave
ROOT\LEGACY_VOLSNAP\0000                                    : VolSnap
ROOT\LEGACY_WANARP\0000                                     : Remote Access IP ARP Driver
27 matching device(s) found.
```

### <span id="ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools"></span><span id="DDK_EXAMPLE_22_FIND_AND_FIND_ALL_DEVICES_IN_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools"></a>示例 22:查找 （并查找所有） 安装程序类中的设备

下面的命令使用[ **DevCon FindAll** ](devcon-findall.md)操作的净安装程序类中的计算机上查找所有设备。 等号 (**=**) 指示 Net 是安装程序类而不是 id。

```
devcon findall =net
```

在响应中，DevCon 列出了中的净安装程序类的以下七个设备。 前六个是标准的微型端口驱动程序设备。 第七个设备，RAS 异步适配器，是软件枚举设备 (SW\\\*) 需要时未安装。

```
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0: 3Com 3C920 Integrated Fast
Ethernet Controller (3C905C-TX Compatible)
ROOT\MS_L2TPMINIPORT\0000                                   : WAN Miniport (L2TP)
ROOT\MS_NDISWANIP\0000                                      : WAN Miniport (IP)
ROOT\MS_PPPOEMINIPORT\0000                                  : WAN Miniport (PPPOE)
ROOT\MS_PPTPMINIPORT\0000                                   : WAN Miniport (PPTP)
ROOT\MS_PTIMINIPORT\0000                                    : Direct Parallel
SW\{EEAB7790-C514-11D1-B42B-00805FC1270E}\ASYNCMAC          : RAS Async Adapter
7 matching device(s) found.
```

下面的命令进行比较[ **DevCon 查找**](devcon-find.md)并**DevCon FindAll**操作通过运行**DevCon 查找**命令具有相同与以前的参数**DevCon FindAll**命令。

```
devcon find =net
```

在响应中，DevCon 列出了以下六个设备中的净安装程序类。

```
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0: 3Com 3C920 Integrated Fast
Ethernet Controller (3C905C-TX Compatible)
ROOT\MS_L2TPMINIPORT\0000                                   : WAN Miniport (L2TP)
ROOT\MS_NDISWANIP\0000                                      : WAN Miniport (IP)
ROOT\MS_PPPOEMINIPORT\0000                                  : WAN Miniport (PPPOE)
ROOT\MS_PPTPMINIPORT\0000                                   : WAN Miniport (PPTP)
ROOT\MS_PTIMINIPORT\0000                                    : Direct Parallel
6 matching device(s) found.
```

以可预测的方式， **DevCon 查找**命令，这将返回仅当前安装的设备，不会列出软件枚举设备，因为未安装该设备。

### <span id="ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools"></span><span id="DDK_EXAMPLE_23_DISPLAY_THE_FILTER_DRIVERS_FOR_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools"></a>示例 23:显示安装程序类的筛选器驱动程序

下面的命令使用[ **DevCon ClassFilter** ](devcon-classfilter.md)操作来显示磁盘驱动器安装程序类的上部的筛选器驱动程序。 因为此命令不包含任何 classfilter 运算符，DevCon 显示类中，筛选器驱动程序，但不会更改。

```
devcon classfilter DiskDrive upper
```

在响应中，DevCon 显示磁盘驱动器类上的筛选器驱动程序，并确认，它未对其进行更改。 在这种情况下，屏幕将显示磁盘驱动器安装程序类中的设备使用 PartMgr.sys 上部的筛选器驱动程序。

```
Class filters unchanged.
    PartMgr
```

### <span id="ddk_example_24_add_a_filter_driver_to_a_setup_class_tools"></span><span id="DDK_EXAMPLE_24_ADD_A_FILTER_DRIVER_TO_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_24_add_a_filter_driver_to_a_setup_class_tools"></a>示例是 24:将筛选器驱动程序添加到安装程序类

下面的命令使用[ **DevCon ClassFilter** ](devcon-classfilter.md)操作可将虚构的筛选器，Disklog.sys，添加到上部的筛选器驱动程序的磁盘驱动器安装程序类的列表。

此命令使用添加之后 (**+**) ClassFilter 运算符后 PartMgr 驱动程序加载 Disklog 驱动程序，以使其接收 PartMgr.sys 已处理的数据。

该命令在启动时，虚拟游标位于第一个筛选器驱动程序之前。 因为它不定位在的特定驱动程序上，DevCon 将 Disklog 驱动程序添加到筛选器驱动程序列表的末尾。

该命令还使用 **/r**参数，它会重新启动系统，如有必要以使类筛选器更改生效。

```
devcon /r classfilter DiskDrive upper +Disklog
```

在响应中，DevCon 显示磁盘驱动器类的当前上部的筛选器驱动程序。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    Disklog
```

如果您拼写错误的驱动程序名称，或尝试添加不在系统安装的驱动程序，该命令将失败。 DevCon 不会添加一个驱动程序除非驱动程序，即注册为服务，除非该驱动程序在服务注册表子项具有一个子项 (HKEY\_本地\_MACHINE\\系统\\CurrentControlSet\\服务)。

以下命令测试此保护功能。 它尝试将"Disklgg"（而不是"Disklog") 添加到上部的筛选器的磁盘驱动器类的列表。 输出表明，该命令将失败。

```
devcon /r classfilter DiskDrive upper +Disklgg
devcon failed.
```

### <span id="ddk_example_25_insert_a_filter_driver_in_the_class_list_tools"></span><span id="DDK_EXAMPLE_25_INSERT_A_FILTER_DRIVER_IN_THE_CLASS_LIST_TOOLS"></span><a name="ddk_example_25_insert_a_filter_driver_in_the_class_list_tools"></a>示例 25:类列表中插入筛选器驱动程序

下面的命令使用[ **DevCon ClassFilter** ](devcon-classfilter.md)操作可将虚构的筛选器驱动程序，MyFilter.sys，添加到上部的筛选器驱动程序的磁盘驱动器安装程序类的列表。 该命令将 PartMgr.sys 和 Disklog.sys 之间 MyFilter.sys 置于的加载顺序。

```
devcon /r classfilter DiskDrive upper @Disklog -MyFilter
```

以下列表显示磁盘驱动器类的筛选器驱动程序，然后提交该命令。

```
    PartMgr
    Disklog
```

第一个子命令， <strong>@Disklog</strong>，使用定位运算符 (**@**) 若要将虚拟光标置于 Disklog 筛选器驱动程序。 第二个子命令， **-MyFilter**，使用添加的运算符之前 (**-**) 以添加之前 Disklog.sys MyFilter.sys。

该命令还使用 **/r**参数，它会重新启动系统，如有必要以使类筛选器更改生效。

在此示例中，定位运算符至关重要。 DevCon 处理任何 classfilter 子命令之前，虚拟光标位于列表的开头，并没有定位在任何筛选器驱动程序上。 如果您使用添加-之前 (**+**) 运算符时光标不在定位的驱动程序、 DevCon 将驱动程序添加到列表的开头。 如果使用添加之后 (**-**) 运算符时游标未定位的驱动程序，它将驱动程序添加到列表的末尾。

在响应中，DevCon 显示磁盘驱动器类的当前上部的筛选器驱动程序。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    MyFilter
    Disklog
```

若要添加 MyFilter 驱动程序，并将其放置 PartMgr 和 Disklog 之间，也可以使用以下命令。 在此示例中，第一个子命令， <strong>@PartMgr</strong>，虚拟将光标定位 PartMgr 筛选器驱动程序。 第二个子命令， **+ MyFilter**，使用添加后运算符 （+） 来添加 MyFilter.sys PartMgr 后。

```
devcon /r classfilter DiskDrive upper @PartMgr +MyFilter
```

### <span id="ddk_example_26_replace_a_filter_driver_tools"></span><span id="DDK_EXAMPLE_26_REPLACE_A_FILTER_DRIVER_TOOLS"></span><a name="ddk_example_26_replace_a_filter_driver_tools"></a>示例 26:替换为筛选器驱动程序

下面的命令使用[ **DevCon ClassFilter** ](devcon-classfilter.md) MyFilter.sys 的原始副本将替换为新的和改进版本，MyNewFilter.sys，在筛选器驱动程序列表中的操作磁盘驱动器安装程序类。

```
devcon /r classfilter DiskDrive upper !MyFilter +MyNewFilter
```

以下列表显示磁盘驱动器类的筛选器驱动程序，然后提交该命令。

```
    PartMgr
    MyFilter
    Disklog
```

第一个子命令使用 delete 运算符 (**！**) 若要从磁盘驱动器类上的筛选器驱动程序列表中删除 MyFilter。 (它不会影响在 c： 驱动器中的 MyFilter.sys 文件\\Windows\\System32\\驱动程序目录。)

第二个子命令使用添加后运算符 (**+**) 将新的筛选器驱动程序放置在已删除的驱动程序所占据的位置。 由于 delete 运算符离开的位置中的光标的已删除的筛选器已被占用，添加-之前 (**-**) 和添加之后 (**+**) 运算符具有相同的效果。)

该命令还使用 **/r**参数，它会重新启动系统，如有必要以使类筛选器更改生效。

在响应中，DevCon 显示磁盘驱动器类的新类筛选器配置。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    MyNewFilter
    Disklog
```

### <span id="ddk_example_27_change_the_order_of_filter_drivers_tools"></span><span id="DDK_EXAMPLE_27_CHANGE_THE_ORDER_OF_FILTER_DRIVERS_TOOLS"></span><a name="ddk_example_27_change_the_order_of_filter_drivers_tools"></a>示例 27:更改筛选器驱动程序的顺序

下面的命令使用[ **DevCon ClassFilter** ](devcon-classfilter.md)操作以更改磁盘驱动器安装程序类的筛选器驱动程序的顺序。 具体而言，它反转第二个和第三个筛选器驱动程序的顺序。

```
devcon /r classfilter DiskDrive upper !Disklog =@PartMgr +Disklog
```

以下列表显示磁盘驱动器类的筛选器驱动程序，然后提交该命令。 它还显示该命令的预期的结果。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">之前</th>
<th align="left">调整后的文本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PartMgr</p></td>
<td align="left"><p>PartMgr</p></td>
</tr>
<tr class="even">
<td align="left"><p>MyNewFilter</p></td>
<td align="left"><p>Disklog</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Disklog</p></td>
<td align="left"><p>MyNewFilter</p></td>
</tr>
</tbody>
</table>

 

第一个子命令使用 delete 运算符 (**！)** 若要从列表中删除 Disklog。 第二个子命令使用开始运算符 (**=)** 若要将虚拟游标移回起始位置，然后使用定位运算符 (**@)** 若要将光标置于 PartMgr 驱动程序。 开始运算符是必要的因为虚拟游标只向前移动列表。 最后一个子命令使用添加后运算符 (**+)** PartMgr 后面添加 Disklog。

在响应中，DevCon 显示磁盘驱动器类的新类筛选器配置。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    Disklog
    MyNewFilter
```

### <span id="ddk_example_28_enable_a_particular_device_tools"></span><span id="DDK_EXAMPLE_28_ENABLE_A_PARTICULAR_DEVICE_TOOLS"></span><a name="ddk_example_28_enable_a_particular_device_tools"></a>示例 28:启用特定设备

下面的命令使用[ **DevCon 启用**](devcon-enable.md)启用已被禁用，以解决系统问题的可编程中断控制器操作。 因为控制器硬件 ID \*PNP0000 包括星号，该命令使用单引号字符 () 若要指示 DevCon 命令中指定一样准确查找的硬件 ID。 否则，星号将解释为通配符字符。

```
devcon enable '*PNP0000
```

在响应中，DevCon 显示设备的设备实例 ID，并说明必须重新启动系统以启用该设备。

```
ACPI\PNP0000\4&B4063F4&0                                    : Enabled on reboot
Not all of 1 device(s) enabled, at least one requires reboot to complete the operation.
```

正在重新启动系统，或者手动或使用可响应[ **DevCon 重启**](devcon-reboot.md)操作。

以下命令将添加 **/r**到前一命令的参数。 **/R**参数重新启动系统，仅当重新启动的完成操作所必需的。

```
devcon /r enable '*PNP0000
```

在响应中，DevCon 启用设备，然后重新启动系统以使启用生效。

在系统启动时，请使用 DevCon 状态命令确认设备已启用。

```
devcon status '*PNP0000

ACPI\PNP0000\4&B4063F4&0
    Name: Programmable interrupt controller
    Driver is running.
```

### <span id="ddk_example_29_enable_devices_by_class_tools"></span><span id="DDK_EXAMPLE_29_ENABLE_DEVICES_BY_CLASS_TOOLS"></span><a name="ddk_example_29_enable_devices_by_class_tools"></a>示例 29:使设备由类

以下命令通过指定的打印机安装程序类中允许对计算机上的所有打印机设备[ **DevCon 启用**](devcon-enable.md)命令。 该命令包含 **/r**参数，它会重新启动系统，如有必要以使启用生效。

```
devcon /r enable =Printer
```

在响应中，DevCon 显示设备实例 ID 的打印机的打印机类和启用它的报表中找到它。 尽管该命令包含 **/r**参数，系统未重新启动，因为不需要重新启动，以启用打印机。

```
LPTENUM\HEWLETT-PACKARDDESKJET_1120C\1&7530F08&0&LPT1.4        : Enabled
1 device(s) enabled.
```

### <span id="ddk_example_30_disable_devices_by_an_id_pattern_tools"></span><span id="DDK_EXAMPLE_30_DISABLE_DEVICES_BY_AN_ID_PATTERN_TOOLS"></span><a name="ddk_example_30_disable_devices_by_an_id_pattern_tools"></a>示例 30:通过 ID 模式来禁用设备

下面的命令使用[ **DevCon 禁用**](devcon-disable.md)禁用本地计算机上的 USB 设备操作。 它标识设备硬件 ID 模式 (USB\*)。 此模式将匹配任何设备的硬件 ID 或兼容 ID 开头"USB。" 该命令包含 **/r**参数，它会重新启动系统，如有必要以使禁用生效。

**请注意**之前使用 ID 模式来禁用设备，确定哪些设备将受到影响。 若要执行此操作，使用模式在显示命令中，如**devcon 状态 USB\\*** 或 * * devcon hwids USB\\* * *。

 

```
devcon /r disable USB*
```

在响应中，DevCon 显示 USB 设备的设备实例 Id 和报表禁用它们。 尽管该命令包含 **/r**参数，系统未重新启动，因为不需要重新启动以禁用设备。

```
USB\ROOT_HUB\4&2A40B465&0
: Disabled
USB\ROOT_HUB\4&7EFA360&0
: Disabled
USB\VID_045E&PID_0039\5&29F428A4&0&2
: Disabled
3 device(s) disabled.
```

### <span id="ddk_example_31_disable_devices_by_device_instance_id_tools"></span><span id="DDK_EXAMPLE_31_DISABLE_DEVICES_BY_DEVICE_INSTANCE_ID_TOOLS"></span><a name="ddk_example_31_disable_devices_by_device_instance_id_tools"></a>示例 31:禁用设备通过设备实例 ID

下面的命令使用[ **DevCon 禁用**](devcon-disable.md)禁用本地计算机上的 USB 设备操作。 此命令其设备实例 Id 来标识设备，如所示在字符 (**@**) 位于每个 id。 与其他由空格分隔每个设备实例 ID。

此外，因为设备实例 Id 包括 & 号字符 (**&**)，它们用引号引起来。 该命令包含 **/r**参数，它会重新启动系统，如有必要以使禁用生效。

```
devcon /r disable "@USB\ROOT_HUB\4&2A40B465&0" "@USB\ROOT_HUB\4&7EFA360&0" "@USB\VID_045E&PID_0039\5&29F428A4&0&2"
```

在响应中，DevCon 显示 USB 设备的设备实例 Id 和报表禁用它们。 尽管该命令包含 **/r**参数，系统未重新启动，因为不需要重新启动以禁用设备。

```
USB\ROOT_HUB\4&2A40B465&0
: Disabled
USB\ROOT_HUB\4&7EFA360&0
: Disabled
USB\VID_045E&PID_0039\5&29F428A4&0&2
: Disabled
3 device(s) disabled.
```

### <span id="ddk_example_32_update_the_driver_for_communication_ports_tools"></span><span id="DDK_EXAMPLE_32_UPDATE_THE_DRIVER_FOR_COMMUNICATION_PORTS_TOOLS"></span><a name="ddk_example_32_update_the_driver_for_communication_ports_tools"></a>示例 32:通信端口的驱动程序更新

下面的命令使用[ **DevCon 更新**](devcon-update.md)操作替换 test.inf 文件中指定的测试驱动程序在系统上的通信端口的当前设备驱动程序。 该命令会影响其整个硬件 id 的设备\*PNP0501 （包括星号）。

在系统上签名的驱动程序替换为备用驱动程序进行测试或故障排除，或将设备与最新版本的相同的驱动程序相关联，可以使用此命令。

```
devcon update c:\windows\inf\test.inf *PNP0501
```

在响应中，显示 DevCon**硬件安装**警告说明该驱动程序尚未通过 Windows 徽标测试。 如果单击**仍然继续**按钮上的对话框中，安装将继续进行。

然后，DevCon 显示以下成功消息。

```
Updating drivers for *PNP0501 from c:\windows\inf\test.inf.
Drivers updated successfully.
```

此外可以使用[ **DevCon UpdateNI** ](devcon-updateni.md)的非交互式版本、 操作**DevCon 更新**操作，更新驱动程序。 **DevCon UpdateNI**操作等同于**DevCon 更新**操作，但它取消需要响应的所有用户提示，并假定默认响应提示。

下面的命令使用**DevCon UpdateNI**操作以安装测试驱动程序。

```
devcon updateni c:\windows\inf\test.inf *PNP0501
```

在这种情况下，未显示 DevCon**硬件安装**警告。 相反，它假定默认响应，因此**停止安装**。 因此，DevCon 不能更新的驱动程序，并显示失败消息。

```
Updating drivers for *PNP0501 from c:\windows\inf\test.inf.
devcon failed.
```

### <span id="ddk_example_33_install_a_device_tools"></span><span id="DDK_EXAMPLE_33_INSTALL_A_DEVICE_TOOLS"></span><a name="ddk_example_33_install_a_device_tools"></a>示例 33:安装设备

下面的命令使用[ **DevCon 安装**](devcon-install.md)操作在本地计算机上安装的键盘设备。 该命令包含设备 (keyboard.inf) 和硬件 ID 的 INF 文件的完整路径 (\*PNP030b)。

```
devcon /r install c:\windows\inf\keyboard.inf *PNP030b
```

在响应中，DevCon 报告它已安装设备，即，其创建新的设备的设备节点和更新的设备驱动程序文件。

```
Device node created. Install is complete when drivers files are updated...
Updating drivers for *PNPO30b from c:\windows\inf\keyboard.inf
Drivers updated successfully.
```

### <span id="ddk_example_34_install_a_device_using_unattended_setup_tools"></span><span id="DDK_EXAMPLE_34_INSTALL_A_DEVICE_USING_UNATTENDED_SETUP_TOOLS"></span><a name="ddk_example_34_install_a_device_using_unattended_setup_tools"></a>示例 34:安装使用无人参与的安装的设备

下面的示例演示如何在 Microsoft Windows XP 无人参与安装过程中安装 Microsoft Loopback 适配器。

若要在无人参与安装过程中安装此设备，首先将以下文件添加到软盘： devcon.exe 和 netloop.inf (c:\\Windows\\inf\\netloop.inf)。

然后，向**\[GUIRunOnce\]** 节的无人参与的安装文件中，添加以下 DevCon 命令：

```
a:\devcon /r install a:\Netloop.inf '*MSLOOP
```

此命令使用其硬件 ID 来标识环回适配器\*MSLOOP。 前面的单引号字符"\*MSLOOP"告知 DevCon，它是按字面意思解释该字符串，以解释星号作为硬件 ID 的一部分，而不是通配符字符。

在安装中，该命令还指定 DevCon 使用 Netloop.inf 文件 （在软盘）。 **/R**如果重新启动完成安装所需参数将计算机重新启动。

最后，将网络配置设置添加到无人参与的安装文件并运行无人参与的安装程序。

### <span id="ddk_example_35_remove_devices_by_device_instance_id_pattern_tools"></span><span id="DDK_EXAMPLE_35_REMOVE_DEVICES_BY_DEVICE_INSTANCE_ID_PATTERN_TOOLS"></span><a name="ddk_example_35_remove_devices_by_device_instance_id_pattern_tools"></a>示例 35:通过设备实例 ID 模式中删除的设备

下面的命令使用[ **DevCon 删除**](devcon-remove.md)操作以从计算机中删除所有 USB 设备。 它标识设备通过任何设备实例 ID （注册表路径） 开头的相匹配的设备实例 ID 模式"USB\\"字符串。 在字符 (**@**) 设备实例 ID 区分开来的硬件 ID 或兼容 id。 该命令还包括 **/r**参数，它会需要它以使该删除过程生效的情况下重新启动系统。

**警告**删除之前的任何设备使用一种模式，请确定哪些设备会受到影响。 若要执行此操作，使用模式在显示命令中，如<strong>devcon 状态@usb \\ \</ s > * 或<strong>devcon hwids @usb \\ \</ s > *。

 

```
devcon /r remove @usb\*
```

在响应中，DevCon 显示将其删除的设备的设备实例 ID。

```
USB\ROOT_HUB\4&2A40B465&0                             : Removed
USB\ROOT_HUB\4&7EFA360&0                              : Removed
USB\VID_045E&PID_0039\5&29F428A4&0&2                  : Removed
3 device(s) removed.
```

### <span id="ddk_example_36_remove_a_particular_network_device_tools"></span><span id="DDK_EXAMPLE_36_REMOVE_A_PARTICULAR_NETWORK_DEVICE_TOOLS"></span><a name="ddk_example_36_remove_a_particular_network_device_tools"></a>示例 36:删除特定网络设备

下面的命令使用[ **DevCon 删除**](devcon-remove.md)操作以从本地计算机上卸载 NDISWAN 微型端口驱动程序。 命令指定的净类，然后通过指定设备的硬件 ID 或兼容 ID 包括"ndiswan。"在类中对搜索进行优化 该命令还包括 **/r**参数，它会重新启动所需使删除过程生效的情况下重新启动系统。

**警告**删除之前的任何设备使用一种模式，请确定哪些设备将受到影响。 若要执行此操作，使用模式在显示命令中，如**devcon 状态 = net \*ndiswan\\*** 或 * * devcon hwids = net \*ndiswan\\* * *。

 

```
devcon /r remove =net *ndiswan*
```

在响应中，DevCon 显示将其删除的设备的设备实例 ID。

```
ROOT\MS_NDISWANIP\0000 : Removed 1 device(s) removed.
```

### <span id="ddk_example_37_scan_the_computer_for_new_devices_tools"></span><span id="DDK_EXAMPLE_37_SCAN_THE_COMPUTER_FOR_NEW_DEVICES_TOOLS"></span><a name="ddk_example_37_scan_the_computer_for_new_devices_tools"></a>示例 37:扫描计算机以查找新设备

下面的命令使用[ **DevCon 重新扫描**](devcon-rescan.md)操作来扫描本地计算机上的新设备。

```
devcon rescan
```

DevCon 报告其扫描系统在响应中，但找到任何新设备。

```
Scanning for new hardware.
Scanning completed.
```

此外可以使用**DevCon 重新扫描**命令在远程计算机上。 以下命令将运行**DevCon 重新扫描**Server01 上的操作，远程计算机，通过添加 **/m**命令参数。

```
devcon /m:\\server01 rescan
```

### <span id="ddk_example_38_restart_a_device_tools"></span><span id="DDK_EXAMPLE_38_RESTART_A_DEVICE_TOOLS"></span><a name="ddk_example_38_restart_a_device_tools"></a>示例 38:重启设备

下面的命令使用[ **DevCon 重启**](devcon-restart.md)操作以重新启动本地计算机上的环回适配器。 该命令限制搜索的净安装程序类，并使该类中指定的设备实例 ID 环回适配器**根\\\*MSLOOP\\0000**。 在字符 (**@**) 标识字符串作为设备实例 id。 单引号字符 ()，该请求文本搜索，可防止 DevCon 解释为通配符字符的 ID 中的星号。

```
devcon restart =net @'ROOT\*MSLOOP\0000
```

在响应中，DevCon 显示设备的设备实例 ID，并将结果报告。

```
ROOT\*MSLOOP\0000                                              : Restarted
1 device(s) restarted.
```

### <span id="ddk_example_39_reboot_the_local_computer_tools"></span><span id="DDK_EXAMPLE_39_REBOOT_THE_LOCAL_COMPUTER_TOOLS"></span><a name="ddk_example_39_reboot_the_local_computer_tools"></a>示例 39:重新启动本地计算机

下面的命令使用[ **DevCon 重启**](devcon-reboot.md)重新启动本地计算机上的操作系统并将在重新启动与硬件安装关联的操作。 与不同 **/r**参数， **DevCon 重启**操作不依赖于另一个操作的返回代码。

可以在脚本和需要系统重新启动的批处理文件中包含此命令。

```
devcon reboot
```

在响应中，DevCon 显示一条消息，指示它正在重新启动计算机 （正在重新启动本地计算机）。


DevCon 使用标准**ExitWindowsEx**函数以重新启动。 如果用户已在计算机上打开的文件或程序将不会关闭，直到用户已答复了系统提示，关闭文件或结束该进程不重新启动系统。

### <span id="ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools"></span><span id="DDK_EXAMPLE_40_ASSIGN_A_HARDWARE_ID_TO_A_LEGACY_DEVICE_TOOLS"></span><a name="ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools"></a>示例 40:将硬件 ID 分配给旧的设备

下面的命令使用[ **DevCon SetHwID** ](devcon-sethwid.md)操作分配的硬件 ID，提示音，到旧版鸣叫设备。

该命令使用设备实例 ID 的设备，根\\旧\_提示音\\0000，因为提示音旧设备不具有任何硬件 Id 或兼容 Id。 它使用在字符 (**@**) 以指示该字符串是一个设备实例 id。

该命令不使用任何符号参数来定位该 id。 默认情况下，DevCon 硬件 ID 列表的末尾添加新的硬件 Id。 在这种情况下，因为该设备已没有其他硬件 Id，位置是不相关。

```
devcon sethwid @ROOT\LEGACY_BEEP\0000 := beep
```

在响应中，DevCon 显示一个消息指示，它会添加到设备的硬件 ID 列表提示音。 它还显示生成的硬件 ID 列表。 在这种情况下，不存在只有一个硬件 ID 列表中。

```
ROOT\LEGACY_BEEP\0000                              : beep
Modified 1 hardware ID(s).
```

### <span id="ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com"></span><span id="DDK_EXAMPLE_41_ADD_A_HARDWARE_ID_TO_ALL_LEGACY_DEVICES_ON_A_REMOTE_COM"></span><a name="ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com"></a>示例 41:添加到远程计算机上的所有旧设备的硬件 ID

下面的命令使用[ **DevCon SetHwID** ](devcon-sethwid.md)操作来添加硬件 ID，旧，到为 Server1 的远程计算机上的所有旧设备的硬件 Id 列表。

该命令使用**-** 符号参数来将新的硬件 ID 添加到该设备，硬件 ID 列表的末尾，以防首选的硬件 ID 创建一个设备。 它使用 **/m**参数来指定远程计算机。 它还使用设备实例 ID 模式中， <strong> @ROOT\\旧\</ s ><em>，以便标识计算机，其设备实例 ID 开头，它是所有的设备上的旧设备 **根\\旧版</em>*。

```
devcon /m:\\Server1 sethwid @ROOT\LEGACY* := -legacy
```

在响应中，DevCon 显示所有受影响的设备生成的硬件 ID 列表。

```
ROOT\LEGACY_AFD\0000                                        : legacy
ROOT\LEGACY_BEEP\0000                                    : beep,legacy
ROOT\LEGACY_CRCDISK\0000                                    : legacy
ROOT\LEGACY_DMBOOT\0000                                     : legacy
ROOT\LEGACY_DMLOAD\0000                                     : legacy
ROOT\LEGACY_FIPS\0000                                       : legacy
...
ROOT\LEGACY_WANARP\0000                                     : legacy
Modified 27 hardware ID(s).
```

将相同的硬件 ID 分配给一组设备后，可以使用其他 DevCon 操作来查看和更改单个命令中的设备。

例如，以下命令显示的所有旧设备的状态。

```
devcon status legacy
```

### <span id="ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot"></span><span id="DDK_EXAMPLE_42_DELETE_A_HARDWARE_ID_FROM_ALL_LEGACY_DEVICES_ON_A_REMOT"></span><a name="ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot"></a>示例 42:从远程计算机上的所有旧设备中删除硬件 ID

下面的命令使用[ **DevCon SetHwID** ](devcon-sethwid.md)操作以删除硬件 ID**旧**，从列表中为 Server1 遥控器上的所有旧设备的硬件 Id计算机。

该命令使用 **/m**参数来指定远程计算机。 它使用硬件 ID**旧**，以便标识所有设备具有该硬件 id。 然后，它使用 **！** 若要删除的符号参数**旧**硬件 id。

```
devcon /m:\\Server1 sethwid legacy := !legacy
```

在响应中，DevCon 显示所有受影响的设备生成的硬件 ID 列表。

```
ROOT\LEGACY_AFD\0000                                        :
ROOT\LEGACY_BEEP\0000                                    : beep
ROOT\LEGACY_CRCDISK\0000                                    :
ROOT\LEGACY_DMBOOT\0000                                     :
ROOT\LEGACY_DMLOAD\0000                                     :
ROOT\LEGACY_FIPS\0000                                       :
...
ROOT\LEGACY_WANARP\0000                                     :
Modified 27 hardware ID(s).
```

### <span id="ddk_example_43_add_delete_and_replace_hardwareids_tools"></span><span id="DDK_EXAMPLE_43_ADD_DELETE_AND_REPLACE_HARDWAREIDS_TOOLS"></span><a name="ddk_example_43_add_delete_and_replace_hardwareids_tools"></a>示例 43:添加、 删除和替换的硬件 Id

以下一系列的示例演示如何使用不同的功能[ **DevCon SetHwID** ](devcon-sethwid.md)操作。

此序列具有设备实例 ID，使用虚构的设备，DeviceX，**根\\DeviceX\\0000**。 在使用 DevCon 以前, 设备具有以下硬件 Id 的列表：

```
Hw3 Hw4
```

下面的命令使用**+** 符号添加**Hw1**并**Hw2**到 DeviceX 的硬件 Id 列表的起始点。 因为**Hw2**已出现在列表中，被移动、 未添加。 该命令按设备实例 ID，将设备标识，由在字符 (**@**) 前面的 id。

```
devcon sethwid @ROOT\DEVICEX\0000 := +Hw1 Hw2
```

在响应中，DevCon 显示设备的新硬件 ID 列表。 请注意， **Hw1**并**Hw2**出现在指定的顺序列表的开头。

```
ROOT\DEVICEX\0000                         : Hw1,Hw2,Hw3,Hw4
Modified 1 hardware ID(s).
```

此外，DevCon 报告其修改一个硬件 ID 列表中，即，硬件 ID 列表的一台设备。

下面的命令使用 **！** 若要删除的符号**Hw1**硬件 id。 然后，列出硬件 ID **Hw5**，不带符号参数。 不带符号参数 SetHwID 将硬件 ID 添加到设备硬件 ID 列表的末尾。

此命令演示，与不同的其他符号参数**DevCon SetHwID**操作， **！** 符号仅适用于它加上前缀的硬件 ID。

```
devcon sethwid @ROOT\DeviceX\0000 := !Hw1 Hw5
```

在响应中，DevCon DeviceX 显示生成的硬件 ID 列表。

```
ROOT\DEVICEX\0000                         : Hw2,Hw3,Hw4,Hw5
Modified 1 hardware ID(s).
```

下面的命令使用 = 参数来替换所有硬件 Id 列表中的为提供了单个硬件 ID，DeviceX **DevX**。

```
devcon sethwid @ROOT\DeviceX\0000 := =DevX
```

在响应中，DevCon DeviceX 显示生成的硬件 ID 列表。

```
ROOT\DEVICEX\0000                         : DevX
Modified 1 hardware ID(s).
```

成功消息指示 DevCon 修改一个设备的硬件 ID。

### <span id="ddk_example_44_forcibly_update_the_hal_tools"></span><span id="DDK_EXAMPLE_44_FORCIBLY_UPDATE_THE_HAL_TOOLS"></span><a name="ddk_example_44_forcibly_update_the_hal_tools"></a>示例 44:强制更新 HAL

下面的示例演示如何使用 DevCon 更新的计算机上的 HAL。 在此示例中，测试人员希望替换单处理器 APCI APIC HAL 最适合与多处理器的 APCI APIC HAL 计算机以进行测试。

第一个命令使用[ **DevCon SetHwID** ](devcon-sethwid.md)操作以更改从 HAL 的硬件 ID **acpiapic\_向上**，单处理器 Hal，则硬件 ID向**acpiapic\_mp**，多处理器 Hal 的硬件 ID。

因为 HAL 的 INF 文件包含单处理器和多处理器 Hal 的驱动程序，则必须更改硬件 ID。 系统将从基于设备的硬件 ID 的 INF 文件选择最合适的驱动程序。 如果不更改的硬件 ID，则**DevCon 更新**命令将只需重新安装单处理器 HAL 驱动程序。

在以下命令中，该命令标识由其实例 ID，HAL**根\\ACPI\_HAL\\0000**，如下所示通过**@** 字符前面的 id。 该命令使用**+** 字符以做出**acpiapic\_mp** HAL 的列表中的第一个硬件 ID。 然后，它使用 **！** 若要删除的字符**acpiapic\_向上**的 HAL Id 列表中的硬件 ID。

```
devcon sethwid @ROOT\ACPI_HAL\0000 := +acpiapic_mp !acpiapic_up
```

在响应中，DevCon HAL 显示以下新的硬件 ID 列表。

```
ROOT\ACPI_HAL\0000                         : acpiapic_mp
Modified 1 hardware ID(s).
```

下面的命令使用[ **DevCon 更新**](devcon-update.md) HAL 有关更新驱动程序的操作。

```
devcon update c:\windows\inf\hal.inf acpiapic_mp
```

然后，DevCon 显示以下成功消息。

```
Updating drivers for acpiapic_mp from c:\windows\inf\hal.inf.
Drivers updated successfully.
```

 

 





