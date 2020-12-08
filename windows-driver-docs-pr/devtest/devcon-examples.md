---
title: 设备控制台 (DevCon.exe) 示例
description: 设备控制台 (DevCon.exe) 示例
keywords:
- DevCon WDK，示例
- 设备控制台 WDK，示例
- 示例 WDK DevCon
- DevCon WDK，命令
- 设备控制台 WDK，命令
- 命令 WDK DevCon
- 示例44强制更新 HAL
- HAL 更新示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a3962a136710751dfcead6ecb9d12511514fe97
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783405"
---
# <a name="device-console-devconexe-examples"></a>设备控制台 (DevCon.exe) 示例


## <span id="ddk_devcon_examples_tools"></span><span id="DDK_DEVCON_EXAMPLES_TOOLS"></span>


本部分提供了下列设备控制台 ( # A0) 命令的示例：

### <a name="span-iddevcon_hwidsspanspan-iddevcon_hwidsspandevcon-hwids"></a><span id="devcon_hwids"></span><span id="DEVCON_HWIDS"></span>DevCon Hwid

[示例1：查找所有硬件 Id](#ddk_example_1_find_all_hardware_ids_tools)

[示例2：使用模式查找硬件 Id](#ddk_example_2_find_hardware_ids_by_using_a_pattern_tools)

[示例3：使用类查找硬件 Id](#ddk_example_3_find_hardware_ids_by_using_a_class_tools)

### <a name="span-iddevcon_classesspanspan-iddevcon_classesspandevcon-classes"></a><span id="devcon_classes"></span><span id="DEVCON_CLASSES"></span>DevCon 类

[示例4：在本地计算机上列出类](#ddk_example_4_list_classes_on_the_local_computer_tools)

[示例5：列出远程计算机上的类](#ddk_example_5_list_classes_on_the_remote_computer_tools)

### <a name="span-iddevcon_listclassspanspan-iddevcon_listclassspandevcon-listclass"></a><span id="devcon_listclass"></span><span id="DEVCON_LISTCLASS"></span>DevCon ListClass

[示例6：列出设备安装程序类中的设备](#ddk_example_6_list_the_devices_in_a_device_setup_class_tools)

[示例7：列出远程计算机上多个类中的设备](#ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute)

### <a name="span-iddevcon_driverfilesspanspan-iddevcon_driverfilesspandevcon-driverfiles"></a><span id="devcon_driverfiles"></span><span id="DEVCON_DRIVERFILES"></span>DevCon DriverFiles

[示例8：列出所有驱动程序文件](#ddk_example_8_list_all_driver_files_tools)

[示例9：列出特定设备的驱动程序文件](#ddk_example_9_list_the_driver_files_of_a_particular_device_tools)

### <a name="span-iddevcon_drivernodesspanspan-iddevcon_drivernodesspandevcon-drivernodes"></a><span id="devcon_drivernodes"></span><span id="DEVCON_DRIVERNODES"></span>DevCon DriverNodes

[示例10：按硬件 ID 模式列出驱动程序包](#ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools)

[示例11：按设备实例 ID 模式列出驱动程序包](#ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool)

### <a name="span-iddevcon_resourcesspanspan-iddevcon_resourcesspandevcon-resources"></a><span id="devcon_resources"></span><span id="DEVCON_RESOURCES"></span>DevCon 资源

[示例12：列出设备类的资源](#ddk_example_12_list_resources_of_a_class_of_devices_tools)

[示例13：按 ID 列出远程计算机上的设备资源](#ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too)

### <a name="span-iddevcon_stackspanspan-iddevcon_stackspandevcon-stack"></a><span id="devcon_stack"></span><span id="DEVCON_STACK"></span>DevCon 堆栈

[示例14：显示存储设备的驱动程序堆栈](#ddk_example_14_display_the_driver_stack_for_storage_devices_tools)

[示例15：查找设备的安装程序类](#ddk_example_15_find_the_setup_class_of_a_device_tools)

[示例16：在远程计算机上显示相关设备的堆栈](#ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu)

### <a name="span-iddevcon_statusspanspan-iddevcon_statusspandevcon-status"></a><span id="devcon_status"></span><span id="DEVCON_STATUS"></span>DevCon 状态

[示例17：显示本地计算机上所有设备的状态](#ddk_example_17_display_the_status_of_all_devices_on_the_local_computer)

[示例18：按设备实例 ID 显示设备状态](#ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to)

[示例19：显示远程计算机上相关设备的状态](#ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu)

### <a name="span-iddevcon_findspanspan-iddevcon_findspandevcon-find"></a><span id="devcon_find"></span><span id="DEVCON_FIND"></span>DevCon 查找

[示例20：按硬件 ID 模式查找设备](#ddk_example_20_find_devices_by_hardware_id_pattern_tools)

[示例21：按设备实例 ID 或类查找设备](#ddk_example_21_find_devices_by_device_instance_id_or_class_tools)

### <a name="span-iddevcon_findallspanspan-iddevcon_findallspandevcon-findall"></a><span id="devcon_findall"></span><span id="DEVCON_FINDALL"></span>DevCon FindAll

[示例22：查找 (并查找安装类中的所有) 设备](#ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools)

### <a name="span-iddevcon_classfilterspanspan-iddevcon_classfilterspandevcon-classfilter"></a><span id="devcon_classfilter"></span><span id="DEVCON_CLASSFILTER"></span>DevCon ClassFilter

[示例23：显示安装程序类的筛选器驱动程序](#ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools)

[示例24：向安装程序类添加筛选器驱动程序](#ddk_example_24_add_a_filter_driver_to_a_setup_class_tools)

[示例25：在类列表中插入筛选器驱动程序](#ddk_example_25_insert_a_filter_driver_in_the_class_list_tools)

[示例26：替换筛选器驱动程序](#ddk_example_26_replace_a_filter_driver_tools)

[示例27：更改筛选器驱动程序的顺序](#ddk_example_27_change_the_order_of_filter_drivers_tools)

### <a name="span-iddevcon_enablespanspan-iddevcon_enablespandevcon-enable"></a><span id="devcon_enable"></span><span id="DEVCON_ENABLE"></span>DevCon 启用

[示例28：启用特定设备](#ddk_example_28_enable_a_particular_device_tools)

[示例29：按类启用设备](#ddk_example_29_enable_devices_by_class_tools)

### <a name="span-iddevcon_disablespanspan-iddevcon_disablespandevcon-disable"></a><span id="devcon_disable"></span><span id="DEVCON_DISABLE"></span>DevCon Disable

[示例30：按 ID 模式禁用设备](#ddk_example_30_disable_devices_by_an_id_pattern_tools)

[示例31：按设备实例 ID 禁用设备](#ddk_example_31_disable_devices_by_device_instance_id_tools)

### <a name="span-iddevcon_update_and_updatenispanspan-iddevcon_update_and_updatenispandevcon-update-and-updateni"></a><span id="devcon_update_and_updateni"></span><span id="DEVCON_UPDATE_AND_UPDATENI"></span>DevCon 更新和 UpdateNI

[示例32：更新通信端口的驱动程序](#ddk_example_32_update_the_driver_for_communication_ports_tools)

[示例44：强制更新 HAL](#ddk_example_44_forcibly_update_the_hal_tools)

### <a name="span-iddevcon_installspanspan-iddevcon_installspandevcon-install"></a><span id="devcon_install"></span><span id="DEVCON_INSTALL"></span>DevCon 安装

[示例33：安装设备](#ddk_example_33_install_a_device_tools)

[示例34：使用无人参与安装程序安装设备](#ddk_example_34_install_a_device_using_unattended_setup_tools)

### <a name="span-iddevcon_removespanspan-iddevcon_removespandevcon-remove"></a><span id="devcon_remove"></span><span id="DEVCON_REMOVE"></span>DevCon 删除

[示例35：按设备实例 ID 模式删除设备](#ddk_example_35_remove_devices_by_device_instance_id_pattern_tools)

[示例36：删除特定网络设备](#ddk_example_36_remove_a_particular_network_device_tools)

### <a name="span-iddevcon_rescanspanspan-iddevcon_rescanspandevcon-rescan"></a><span id="devcon_rescan"></span><span id="DEVCON_RESCAN"></span>DevCon 重新扫描

[示例37：扫描计算机中的新设备](#ddk_example_37_scan_the_computer_for_new_devices_tools)

### <a name="span-iddevcon_restartspanspan-iddevcon_restartspandevcon-restart"></a><span id="devcon_restart"></span><span id="DEVCON_RESTART"></span>DevCon 重启

[示例38：重新启动设备](#ddk_example_38_restart_a_device_tools)

### <a name="span-iddevcon_status2spanspan-iddevcon_status2spandevcon-status"></a><span id="devcon_status2"></span><span id="DEVCON_STATUS2"></span>DevCon 状态

[示例39：重新启动本地计算机](#ddk_example_39_reboot_the_local_computer_tools)

### <a name="span-iddevcon_sethwidspanspan-iddevcon_sethwidspandevcon-sethwid"></a><span id="devcon_sethwid"></span><span id="DEVCON_SETHWID"></span>DevCon SetHwID

[示例40：向旧设备分配硬件 ID](#ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools)

[示例41：向远程计算机上的所有旧设备添加硬件 ID](#ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com)

[示例42：从远程计算机上的所有旧设备中删除硬件 ID](#ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot)

[示例43：添加、删除和替换硬件 Id](#ddk_example_43_add_delete_and_replace_hardwareids_tools)

[示例44：强制更新 HAL](#ddk_example_44_forcibly_update_the_hal_tools)

### <a name="span-iddevcon_dp_add__dp_deleted__dp_enumspanspan-iddevcon_dp_add__dp_deleted__dp_enumspandevcon-dp_add-dp_deleted-dp_enum"></a><span id="devcon_dp_add__dp_deleted__dp_enum"></span><span id="DEVCON_DP_ADD__DP_DELETED__DP_ENUM"></span>DevCon dp \_ add，dp \_ 已删除，dp \_ 枚举

[示例 45：添加和删除驱动程序包](example-45--add-and-remove-driver-packages.md)

### <a name="span-idddk_example_1_find_all_hardware_ids_toolsspanspan-idddk_example_1_find_all_hardware_ids_toolsspanexample-1-find-all-hardware-ids"></a><span id="ddk_example_1_find_all_hardware_ids_tools"></span><span id="DDK_EXAMPLE_1_FIND_ALL_HARDWARE_IDS_TOOLS"></span><a name="ddk_example_1_find_all_hardware_ids_tools"></a>示例1：查找所有硬件 Id

由于 DevCon 操作使用 Id 和 ID 模式来标识设备，因此使用 DevCon 的常见第一步是为计算机上的设备创建硬件 ID 引用文件。

以下命令使用 [**DevCon hwid**](devcon-hwids.md) 操作，该操作将返回 id 和设备描述。 它使用通配符 ( * *\** _) 来表示本地计算机上的所有设备。

```
devcon hwids _
```

由于输出很长并重复使用，因此将输出保存在文本文件中以供参考。

以下命令使用通配符 ( * *\** _) 来表示计算机上的所有设备。它使用重定向字符 (_ <em>&gt;</em> * ) 将命令输出保存到 hwids.txt 文件中。

```
devcon hwids * > hwids.txt
```

以下命令查找远程计算机（Server01）上的设备的硬件 Id。 它使用 **/m** 参数指定远程计算机的名称。 此命令会将输出重定向到 server01 \_hwids.txt 文件，供以后参考。

**注意**   此命令会失败，除非用户在远程计算机上具有所需的权限。 若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和 Windows 7 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 Windows 驱动程序工具包 (WDK) 8.1 和 Windows 驱动程序工具包 (WDK) 8 的计算机上，远程访问不可用。

 

```
devcon /m:\\server01 hwids * > server01_hwids.txt
```

### <a name="span-idddk_example_2_find_hardware_ids_by_using_a_pattern_toolsspanspan-idddk_example_2_find_hardware_ids_by_using_a_pattern_toolsspanexample-2-find-hardware-ids-by-using-a-pattern"></a><span id="ddk_example_2_find_hardware_ids_by_using_a_pattern_tools"></span><span id="DDK_EXAMPLE_2_FIND_HARDWARE_IDS_BY_USING_A_PATTERN_TOOLS"></span><a name="ddk_example_2_find_hardware_ids_by_using_a_pattern_tools"></a>示例2：使用模式查找硬件 Id

若要查找特定设备的硬件 Id，请输入硬件 ID 或模式、兼容 ID 或模式、设备实例 ID 或模式或设备安装程序类的名称。

以下命令使用 **DevCon hwid** 操作和模式来查找计算机上软盘驱动器的硬件 id。  (用户假定模式显示在设备标识符之一中。 ) 此命令使用通配符 ( * *\** _) 来表示任何 id 中的单词 "软盘" 之前或之后的所有字符。

```
devcon hwids _floppy*
```

在响应中，DevCon 显示计算机上软盘驱动器的设备实例 ID、硬件 ID 和兼容 ID。 可以在后续的 DevCon 命令中使用这些 Id。

```
FDC\GENERIC_FLOPPY_DRIVE\5&39194F6D&0&0
    Name: Floppy disk drive
    Hardware ID's:
        FDC\GENERIC_FLOPPY_DRIVE
    Compatible ID's:
        GenFloppyDisk
1 matching device(s) found.
```

在这种情况下，短语 "软盘" 出现在计算机上仅有一个设备的硬件 ID 或兼容 ID 中。 如果在多个设备的 ID 中出现此错误，则其 Id 中的所有设备都显示在输出中。

### <a name="span-idddk_example_3_find_hardware_ids_by_using_a_class_toolsspanspan-idddk_example_3_find_hardware_ids_by_using_a_class_toolsspanexample-3-find-hardware-ids-by-using-a-class"></a><span id="ddk_example_3_find_hardware_ids_by_using_a_class_tools"></span><span id="DDK_EXAMPLE_3_FIND_HARDWARE_IDS_BY_USING_A_CLASS_TOOLS"></span><a name="ddk_example_3_find_hardware_ids_by_using_a_class_tools"></a>示例3：使用类查找硬件 Id

以下命令使用 [**DevCon hwid**](devcon-hwids.md) 操作和设备安装程序类来查找端口设备安装程序类中所有设备的硬件 id。 类名前面的等号 (**=**) 指示它是一个类，而不是 ID。

```
devcon hwids =ports
```

在响应中，DevCon 显示端口安装程序类中三个设备的硬件 Id 和兼容 Id。

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

### <a name="span-idddk_example_4_list_classes_on_the_local_computer_toolsspanspan-idddk_example_4_list_classes_on_the_local_computer_toolsspanexample-4-list-classes-on-the-local-computer"></a><span id="ddk_example_4_list_classes_on_the_local_computer_tools"></span><span id="DDK_EXAMPLE_4_LIST_CLASSES_ON_THE_LOCAL_COMPUTER_TOOLS"></span><a name="ddk_example_4_list_classes_on_the_local_computer_tools"></a>示例4：在本地计算机上列出类

由于 DevCon 操作可以使用设备安装程序类来标识设备，因此，在计算机上创建设备的设备安装程序类的引用文件非常有用。

以下命令使用 [**DevCon 类**](devcon-classes.md) 操作，该操作返回计算机上所有类的列表和说明。

```
devcon classes
```

由于输出很长并重复使用，因此将输出保存在文本文件中以供参考。

以下命令将显示计算机上的所有设备类。 它使用重定向字符 (**&gt;**) 将命令输出保存到 classes.txt 文件中。

```
devcon classes > classes.txt
```

### <a name="span-idddk_example_5_list_classes_on_the_remote_computer_toolsspanspan-idddk_example_5_list_classes_on_the_remote_computer_toolsspanexample-5-list-classes-on-the-remote-computer"></a><span id="ddk_example_5_list_classes_on_the_remote_computer_tools"></span><span id="DDK_EXAMPLE_5_LIST_CLASSES_ON_THE_REMOTE_COMPUTER_TOOLS"></span><a name="ddk_example_5_list_classes_on_the_remote_computer_tools"></a>示例5：列出远程计算机上的类

以下命令使用 [**DevCon 类**](devcon-classes.md) 操作来列出远程计算机上的设备安装程序类，Server01：

```
devcon /m:\\server01 classes
```

由于输出很长并重复使用，因此将输出保存在文本文件中以供参考。

以下命令使用重定向字符 (**&gt;**) 将命令输出保存在 server01 \_classes.txt 文件中。

```
devcon /m:\\server01 classes > server01_classes.txt
```

### <a name="span-idddk_example_6_list_the_devices_in_a_device_setup_class_toolsspanspan-idddk_example_6_list_the_devices_in_a_device_setup_class_toolsspanexample-6-list-the-devices-in-a-device-setup-class"></a><span id="ddk_example_6_list_the_devices_in_a_device_setup_class_tools"></span><span id="DDK_EXAMPLE_6_LIST_THE_DEVICES_IN_A_DEVICE_SETUP_CLASS_TOOLS"></span><a name="ddk_example_6_list_the_devices_in_a_device_setup_class_tools"></a>示例6：列出设备安装程序类中的设备

以下命令使用 [**DevCon ListClass**](devcon-listclass.md) 操作列出网络中的设备，即网络适配器的设备安装程序类。

```
devcon listclass net
```

在响应中，DevCon 显示 Net setup 类中每个设备的设备实例 ID 和描述。

```
Listing 6 device(s) for setup class "Net" (Network adapters).
PCI\VEN_10B7&DEV_9200&SUBSYS_00BE1028&REV_78\4&BB7B4AE&0&60F0: 3Com 3C920 Integrated Fast Ethernet Controller (3C905C-TX Compatible)
ROOT\MS_L2TPMINIPORT\0000                                   : WAN Miniport (L2TP)
ROOT\MS_NDISWANIP\0000                                      : WAN Miniport (IP)
ROOT\MS_PPPOEMINIPORT\0000                                  : WAN Miniport (PPPOE)
ROOT\MS_PPTPMINIPORT\0000                                   : WAN Miniport (PPTP)
ROOT\MS_PTIMINIPORT\0000                                    : Direct Parallel
```

此显示虽然很有趣，但并不提供 Net setup 类中的设备的硬件 Id。 以下命令使用 [**DevCon hwid**](devcon-hwids.md) 操作列出 Net setup 类中的设备。 在 **DevCon hwid** 命令中，类名前面有一个等号 () ， **=** 以指示它是一个类，而不是 ID。

```
devcon hwids =net
```

生成的显示将列出网络类中的设备，并在类中包括设备实例 ID、硬件 Id 和设备的兼容 Id。

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

### <a name="span-idddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_computespanspan-idddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_computespanexample-7-list-the-devices-in-multiple-classes-on-a-remote-computer"></a><span id="ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute"></span><span id="DDK_EXAMPLE_7_LIST_THE_DEVICES_IN_MULTIPLE_CLASSES_ON_A_REMOTE_COMPUTE"></span><a name="ddk_example_7_list_the_devices_in_multiple_classes_on_a_remote_compute"></a>示例7：列出远程计算机上多个类中的设备

以下命令使用 [**DevCon ListClass**](devcon-listclass.md) 操作列出 Server01 上的 DISKDRIVE、CDROM 和 TapeDrive 类中的设备，以及远程计算机。

```
devcon /m:\\server01 listclass diskdrive cdrom tapedrive
```

在响应中，DevCon 显示远程计算机上这些类中的设备。

```
Listing 1 device(s) for setup class "DiskDrive" (Disk drives) on \\server01.
IDE\DISKWDC_WD204BA_____________________________16.13M16\4457572D414D3730323136333938203120202020: WDC WD204BA
Listing 1 device(s) for setup class "CDROM" (DVD/CD-ROM drives) on \\server01.
IDE\CDROMSAMSUNG_DVD-ROM_SD-608__________________2.2_____\4&13B4AFD&0&0.0.0: SAMSUNG DVD-ROM SD-608
No devices for setup class "TapeDrive" (Tape drives) on \\server01.
```

### <a name="span-idddk_example_8_list_all_driver_files_toolsspanspan-idddk_example_8_list_all_driver_files_toolsspanexample-8-list-all-driver-files"></a><span id="ddk_example_8_list_all_driver_files_tools"></span><span id="DDK_EXAMPLE_8_LIST_ALL_DRIVER_FILES_TOOLS"></span><a name="ddk_example_8_list_all_driver_files_tools"></a>示例8：列出所有驱动程序文件

以下命令使用 [**DevCon DriverFiles**](devcon-driverfiles.md) 操作列出系统上设备使用的驱动程序的文件名。 该命令使用通配符 ( * *\** _) 来指示系统上的所有设备。由于输出范围很大，因此该命令使用重定向字符 (_ <em>&gt;</em> * ) 将输出重定向到引用文件，driverfiles.txt。

```
devcon driverfiles * > driverfiles.txt
```

### <a name="span-idddk_example_9_list_the_driver_files_of_a_particular_device_toolsspanspan-idddk_example_9_list_the_driver_files_of_a_particular_device_toolsspanexample-9-list-the-driver-files-of-a-particular-device"></a><span id="ddk_example_9_list_the_driver_files_of_a_particular_device_tools"></span><span id="DDK_EXAMPLE_9_LIST_THE_DRIVER_FILES_OF_A_PARTICULAR_DEVICE_TOOLS"></span><a name="ddk_example_9_list_the_driver_files_of_a_particular_device_tools"></a>示例9：列出特定设备的驱动程序文件

以下命令使用 [**DevCon DriverFiles**](devcon-driverfiles.md) 操作搜索本地计算机上的鼠标设备使用的设备驱动程序。 它通过设备的一个硬件 Id 来标识设备，HID \\ Vid \_ 045E&Pid \_ 0039&Rev \_ 0121。 硬件 ID 以引号括起来，因为它包括与号字符 (**&**) 。

```
devcon driverfiles "HID\Vid_045e&Pid_0039&Rev_0121"
```

在响应中，DevCon 显示两个支持鼠标设备的设备驱动程序。

```
HID\VID_045E&PID_0039\6&DC36FDE&0&0000
    Name: Microsoft USB IntelliMouse Optical
    Driver installed from c:\windows\inf\msmouse.inf [HID_Mouse_Inst]. 2 file(s)
 used by driver:
        C:\WINDOWS\System32\DRIVERS\mouhid.sys
        C:\WINDOWS\System32\DRIVERS\mouclass.sys
1 matching device(s) found.
```

### <a name="span-idddk_example_10_list_driver_packages_by_hardware_id_pattern_toolsspanspan-idddk_example_10_list_driver_packages_by_hardware_id_pattern_toolsspanexample-10-list-driver-packages-by-hardware-id-pattern"></a><span id="ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools"></span><span id="DDK_EXAMPLE_10_LIST_DRIVER_PACKAGES_BY_HARDWARE_ID_PATTERN_TOOLS"></span><a name="ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools"></a>示例10：按硬件 ID 模式列出驱动程序包

以下命令使用 [**DevCon DriverNodes**](devcon-drivernodes.md) 命令和 ID 模式列出软件枚举设备的驱动程序节点。 模式适用于查找有关可能不在同一安装程序类中的类似设备的信息。

以下命令使用 ID 模式 **sw \\** _ 来指定硬件 Id 或兼容 id 以 "sw" 开头的设备，即软件枚举设备。

```
devcon drivernodes sw_
```

在响应中，DevCon 显示系统上软件枚举设备的驱动程序节点。

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

### <a name="span-idddk_example_11_list_driver_packages_by_device_instance_id_pattern_toolspanspan-idddk_example_11_list_driver_packages_by_device_instance_id_pattern_toolspanexample-11-list-driver-packages-by-device-instance-id-pattern"></a><span id="ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool"></span><span id="DDK_EXAMPLE_11_LIST_DRIVER_PACKAGES_BY_DEVICE_INSTANCE_ID_PATTERN_TOOL"></span><a name="ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool"></a>示例11：按设备实例 ID 模式列出驱动程序包

以下命令使用 [**DevCon DriverNodes**](devcon-drivernodes.md) 操作列出其设备实例 ID 以根媒体开头的所有设备的驱动程序包，即 \\ "枚举 \\ 根媒体注册表" 子项中的 "设备" \\ 。 该命令使用位于的 at 字符 (**@**) 来指示该短语在设备实例 ID 中。

```
devcon drivernodes @ROOT\MEDIA*
```

在响应中，DevCon 显示其设备实例 ID 以 "ROOT MEDIA" 开头的设备的驱动程序节点 \\ 。

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

### <a name="span-idddk_example_12_list_resources_of_a_class_of_devices_toolsspanspan-idddk_example_12_list_resources_of_a_class_of_devices_toolsspanexample-12-list-resources-of-a-class-of-devices"></a><span id="ddk_example_12_list_resources_of_a_class_of_devices_tools"></span><span id="DDK_EXAMPLE_12_LIST_RESOURCES_OF_A_CLASS_OF_DEVICES_TOOLS"></span><a name="ddk_example_12_list_resources_of_a_class_of_devices_tools"></a>示例12：列出设备类的资源

以下命令使用 [**DevCon resources**](devcon-resources.md) 操作来显示分配给 Hdc 设备安装程序类中的设备的资源。 此类包含 IDE 控制器。 等号 (**=**) 预置到 "hdc"，以指示它是类而不是 ID。

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

### <a name="span-idddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_toospanspan-idddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_toospanexample-13-list-resources-of-device-on-a-remote-computer-by-id"></a><span id="ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too"></span><span id="DDK_EXAMPLE_13_LIST_RESOURCES_OF_DEVICE_ON_A_REMOTE_COMPUTER_BY_ID_TOO"></span><a name="ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too"></a>示例13：按 ID 列出远程计算机上的设备资源

以下命令使用 [**DevCon Resources**](devcon-resources.md) 操作列出分配给 Server01 （远程计算机）上的系统计时器的资源。 该命令使用系统计时器的硬件 ID （ACPI \\ PNP0100）来指定设备。

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

以下命令使用 DevCon resources 命令中远程系统计时器的设备实例 ID。 位于字符 (**@**) 指示字符串是设备实例 ID，而不是硬件 id 或兼容 ID。

```
devcon /m:\\Server01 resources @ACPI\PNP0100\4&b4063f4&0
```

### <a name="span-idddk_example_14_display_the_driver_stack_for_storage_devices_toolsspanspan-idddk_example_14_display_the_driver_stack_for_storage_devices_toolsspanexample-14-display-the-driver-stack-for-storage-devices"></a><span id="ddk_example_14_display_the_driver_stack_for_storage_devices_tools"></span><span id="DDK_EXAMPLE_14_DISPLAY_THE_DRIVER_STACK_FOR_STORAGE_DEVICES_TOOLS"></span><a name="ddk_example_14_display_the_driver_stack_for_storage_devices_tools"></a>示例14：显示存储设备的驱动程序堆栈

以下命令使用 [**DevCon Stack**](devcon-stack.md) 操作在卷安装程序类中搜索设备，并为这些设备显示预期的驱动程序堆栈。 等号 (**=**) 指示字符串是类名。

```
devcon stack =Volume
```

在响应中，DevCon 显示 Volume 类中设备的预期堆栈。 返回的数据包括设备实例 ID 和每个设备的说明、设备安装程序类的 GUID 和名称、大写和小写筛选器驱动程序的名称，以及控制服务 (如果有任何) 。

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

### <a name="span-idddk_example_15_find_the_setup_class_of_a_device_toolsspanspan-idddk_example_15_find_the_setup_class_of_a_device_toolsspanexample-15-find-the-setup-class-of-a-device"></a><span id="ddk_example_15_find_the_setup_class_of_a_device_tools"></span><span id="DDK_EXAMPLE_15_FIND_THE_SETUP_CLASS_OF_A_DEVICE_TOOLS"></span><a name="ddk_example_15_find_the_setup_class_of_a_device_tools"></a>示例15：查找设备的安装程序类

[**DevCon Stack**](devcon-stack.md)操作除了返回筛选器驱动程序的上限和下限以外，还返回设备的安装程序类。 下面的命令通过查找打印机端口接口的设备实例 ID 并使用设备实例 ID 查找其安装程序类来查找打印机端口接口的安装程序类。

以下命令使用 [**DevCon hwid**](devcon-hwids.md) 操作，通过使用打印机端口硬件 ID 中的短语 "LPT" 查找打印机端口接口的设备实例 ID。

```
devcon hwids *lpt*
```

在响应中，DevCon 返回 (以粗体文本显示的设备实例 ID) 和打印机端口接口的硬件 ID。

```
LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1
    Name: Printer Port Logical Interface
    Hardware ID's:
        LPTENUM\MicrosoftRawPort958A
        MicrosoftRawPort958A
1 matching device(s) found.
```

下一个命令使用 [**DevCon Stack**](devcon-stack.md) 操作查找设备实例 ID 表示的设备的设备安装程序类。 位于字符 (**@**) 将 id 标识为设备实例 id。 ID 用引号引起来，因为它包含 "&" 字符。

```
devcon stack "@LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1"
```

在响应中，DevCon 显示打印机端口接口的驱动程序堆栈，包括类。 此显示显示打印机端口位于系统类中。

```
LPTENUM\MICROSOFTRAWPORT\5&CA97D7E&0&LPT1
    Name: Printer Port Logical Interface
    Setup Class: {4D36E97D-E325-11CE-BFC1-08002BE10318} System
    Controlling service:
        (none)
1 matching device(s) found.
```

### <a name="span-idddk_example_16_display_the_stack_for_related_devices_on_a_remote_compuspanspan-idddk_example_16_display_the_stack_for_related_devices_on_a_remote_compuspanexample-16-display-the-stack-for-related-devices-on-a-remote-computer"></a><span id="ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu"></span><span id="DDK_EXAMPLE_16_DISPLAY_THE_STACK_FOR_RELATED_DEVICES_ON_A_REMOTE_COMPU"></span><a name="ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu"></a>示例16：在远程计算机上显示相关设备的堆栈

以下命令使用 **DevCon stack** 操作来显示 Server01 （远程计算机）上的微型端口驱动程序设备的预期堆栈。 它在 Net setup 类中搜索其硬件 ID 或兼容 ID 中包含 "微型端口" 的设备。

请注意，此命令首先将搜索限制为 Net setup 类，然后查找 "微型端口" 字符串。 它找不到 Net setup 类中的其他设备。

```
devcon /m:\\server01 stack =net *miniport*
```

在响应中，DevCon 在 Server01 上显示微型端口驱动程序的预期堆栈。

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

### <a name="span-idddk_example_17_display_the_status_of_all_devices_on_the_local_computerspanspan-idddk_example_17_display_the_status_of_all_devices_on_the_local_computerspanexample-17-display-the-status-of-all-devices-on-the-local-computer"></a><span id="ddk_example_17_display_the_status_of_all_devices_on_the_local_computer"></span><span id="DDK_EXAMPLE_17_DISPLAY_THE_STATUS_OF_ALL_DEVICES_ON_THE_LOCAL_COMPUTER"></span><a name="ddk_example_17_display_the_status_of_all_devices_on_the_local_computer"></a>示例17：显示本地计算机上所有设备的状态

以下命令使用 [**DevCon 状态**](devcon-status.md) 操作来查找本地计算机上所有设备的状态。 然后，它将状态保存在 status.txt 文件中，以便进行日志记录或以后查看。 该命令使用通配符 ( * *\** _) 来表示所有设备，并使用重定向字符 (_ <em>&gt;</em> * ) 将输出重定向到 status.txt 文件。

```
devcon status * > status.txt
```

### <a name="span-idddk_example_18_display_the_status_of_a_device_by_device_instance_id_tospanspan-idddk_example_18_display_the_status_of_a_device_by_device_instance_id_tospanexample-18-display-the-status-of-a-device-by-device-instance-id"></a><span id="ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to"></span><span id="DDK_EXAMPLE_18_DISPLAY_THE_STATUS_OF_A_DEVICE_BY_DEVICE_INSTANCE_ID_TO"></span><a name="ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to"></a>示例18：按设备实例 ID 显示设备状态

查找特定设备的状态的最可靠方法是使用设备的设备实例 ID。

下面的命令使用使用本地计算机 [**上的 i/o**](devcon-status.md) 控制器的设备实例 ID。 此命令包含设备的设备实例 ID，PCI \\ 即使 \_ 8086&DEV \_ 1130&子系统 \_ 00000000&REV \_ 02 \\ 3&29E81982&0&00。 ID 为的位置 (**@**) 前缀标识作为设备实例 ID 的字符串。 ID 必须用引号引起来，因为它包含 "&" 字符。

```
devcon status "@PCI\VEN_8086&DEV_1130&SUBSYS_00000000&REV_02\3&29E81982&0&00"
```

在响应中，DevCon 显示 i/o 控制器的状态。

```
PCI\VEN_8086&DEV_1130&SUBSYS_00000000&REV_02\3&29E81982&0&00
    Name: Intel(R) 82815 Processor to I/O Controller - 1130
    Driver is running.
1 matching device(s) found.
```

### <a name="span-idddk_example_19_display_the_status_of_related_devices_on_a_remote_compuspanspan-idddk_example_19_display_the_status_of_related_devices_on_a_remote_compuspanexample-19-display-the-status-of-related-devices-on-a-remote-computer"></a><span id="ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu"></span><span id="DDK_EXAMPLE_19_DISPLAY_THE_STATUS_OF_RELATED_DEVICES_ON_A_REMOTE_COMPU"></span><a name="ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu"></a>示例19：显示远程计算机上相关设备的状态

以下命令使用 [**DevCon 状态**](devcon-status.md) 操作来显示 Server01 上的特定存储相关设备（远程计算机）的状态。 它会搜索以下设备：

-   磁盘驱动器，GenDisk

-   CD-ROM 驱动器，GenCdRom

-   软盘驱动器，FDC \\ 通用 \_ 软盘 \_ 驱动器

-   卷，存储 \\ 卷

-   逻辑磁盘管理器，根 \\ DMIO

-   卷管理器，根 \\ FTDISK

-   软盘控制器，ACPI \\ PNP0700

在命令中，每个 ID 都用空格分隔。 请注意，GenDisk 和 GenCdRom 是兼容的 Id，而其他 Id 是硬件 Id。

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

### <a name="span-idddk_example_20_find_devices_by_hardware_id_pattern_toolsspanspan-idddk_example_20_find_devices_by_hardware_id_pattern_toolsspanexample-20-find-devices-by-hardware-id-pattern"></a><span id="ddk_example_20_find_devices_by_hardware_id_pattern_tools"></span><span id="DDK_EXAMPLE_20_FIND_DEVICES_BY_HARDWARE_ID_PATTERN_TOOLS"></span><a name="ddk_example_20_find_devices_by_hardware_id_pattern_tools"></a>示例20：按硬件 ID 模式查找设备

以下命令使用 [**DevCon Find**](devcon-find.md) 操作在 Server01 （远程计算机）上搜索鼠标设备。 具体而言，该命令会在 Server01 计算机中搜索其硬件 ID 或兼容 ID 包含 "mou" 的设备。

```
devcon /m:\\Server01 find *mou*
```

在这种情况下，DevCon 找到两个鼠标设备。

```
ROOT\*PNP0F03\1_0_21_0_31_0                                 : Microsoft PS/2 Mouse
ROOT\RDP_MOU\0000                                           : Terminal Server Mouse Driver
```

由于所有 DevCon 显示操作还会找到硬件 Id，因此你可以使用任何显示操作来搜索硬件 Id。 根据输出中所需的内容选择操作。 例如，若要查找本地计算机上与鼠标相关的设备所使用的设备驱动程序，请提交以下命令。

```
devcon driverfiles *mou*
```

在响应中，DevCon 查找设备并列出其驱动程序。

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

### <a name="span-idddk_example_21_find_devices_by_device_instance_id_or_class_toolsspanspan-idddk_example_21_find_devices_by_device_instance_id_or_class_toolsspanexample-21-find-devices-by-device-instance-id-or-class"></a><span id="ddk_example_21_find_devices_by_device_instance_id_or_class_tools"></span><span id="DDK_EXAMPLE_21_FIND_DEVICES_BY_DEVICE_INSTANCE_ID_OR_CLASS_TOOLS"></span><a name="ddk_example_21_find_devices_by_device_instance_id_or_class_tools"></a>示例21：按设备实例 ID 或类查找设备

以下命令使用 [**DevCon Find**](devcon-find.md) 操作来显示本地计算机上的所有旧设备。 由于旧版设备没有硬件 ID，你必须按其设备实例 ID 搜索它们 (注册表路径) 、根 \\ 旧版或其安装程序类 LegacyDriver。

第一个命令按设备实例 ID 模式查找旧驱动程序。 ID 模式前面是一个字符 (**@**) ，用于指示设备实例 ID，后跟通配符 ( * *\** _) 以查找根旧子项中的所有设备 \\ 。

```
devcon find @root\legacy_
```

第二个命令通过搜索 LegacyDriver 类中的所有设备，查找旧版设备。

```
devcon find =legacydriver
```

这两个命令都生成相同的输出，在本例中，查找相同的27个旧设备。

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

### <a name="span-idddk_example_22_find_and_find_all_devices_in_a_setup_class_toolsspanspan-idddk_example_22_find_and_find_all_devices_in_a_setup_class_toolsspanexample-22-find-and-find-all-devices-in-a-setup-class"></a><span id="ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools"></span><span id="DDK_EXAMPLE_22_FIND_AND_FIND_ALL_DEVICES_IN_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools"></a>示例22：查找 (并查找安装类中的所有) 设备

以下命令使用 [**DevCon FindAll**](devcon-findall.md) 操作在 Net setup 类中查找计算机上的所有设备。 等号 (**=**) 指示 Net 是安装类而不是 ID。

```
devcon findall =net
```

在响应中，DevCon 列出了 Net setup 类中的以下七个设备。 前六个是标准微型端口驱动程序设备。 第七个设备（RAS 异步适配器）是一个软件枚举设备 (SW \\ \*) ，在需要时才会安装。

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

下面的命令通过运行与上一个 **Devcon FindAll** 命令具有相同参数的 **devcon find** 命令来比较 [**devcon find**](devcon-find.md)和 **DevCon FindAll** 操作。

```
devcon find =net
```

在响应中，DevCon 列出了 Net setup 类中的以下六个设备。

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

可预测的 **DevCon Find** 命令（仅返回当前已安装的设备）不会列出软件枚举的设备，因为未安装设备。

### <a name="span-idddk_example_23_display_the_filter_drivers_for_a_setup_class_toolsspanspan-idddk_example_23_display_the_filter_drivers_for_a_setup_class_toolsspanexample-23-display-the-filter-drivers-for-a-setup-class"></a><span id="ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools"></span><span id="DDK_EXAMPLE_23_DISPLAY_THE_FILTER_DRIVERS_FOR_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_23_display_the_filter_drivers_for_a_setup_class_tools"></a>示例23：显示安装程序类的筛选器驱动程序

以下命令使用 [**DevCon ClassFilter**](devcon-classfilter.md) 操作显示 DiskDrive 安装程序类的筛选器驱动程序。 由于此命令不包含任何 classfilter 运算符，因此 DevCon 显示类的筛选器驱动程序，但不更改它们。

```
devcon classfilter DiskDrive upper
```

在响应中，DevCon 显示 DiskDrive 类的筛选器的筛选器驱动程序，并确认其没有更改。 在这种情况下，将显示 DiskDrive 安装程序类中的设备使用 PartMgr.sys 的筛选器驱动程序。

```
Class filters unchanged.
    PartMgr
```

### <a name="span-idddk_example_24_add_a_filter_driver_to_a_setup_class_toolsspanspan-idddk_example_24_add_a_filter_driver_to_a_setup_class_toolsspanexample-24-add-a-filter-driver-to-a-setup-class"></a><span id="ddk_example_24_add_a_filter_driver_to_a_setup_class_tools"></span><span id="DDK_EXAMPLE_24_ADD_A_FILTER_DRIVER_TO_A_SETUP_CLASS_TOOLS"></span><a name="ddk_example_24_add_a_filter_driver_to_a_setup_class_tools"></a>示例24：向安装程序类添加筛选器驱动程序

以下命令使用 [**DevCon ClassFilter**](devcon-classfilter.md) 操作向 DiskDrive 安装程序类的上层筛选器驱动程序列表中添加虚构筛选器 Disklog.sys。

此命令使用 "外接程序 (" **+**) ClassFilter "运算符在 PartMgr 驱动程序之后加载 Disklog 驱动程序，以便接收 PartMgr.sys 已经处理的数据。

命令启动时，虚拟游标位于第一个筛选器驱动程序之前。 因为它没有定位在特定的驱动程序上，所以 DevCon 会将 Disklog 驱动程序添加到筛选器驱动程序列表的末尾。

该命令还使用 **/r** 参数，如果需要使类筛选器更改生效，则会重新启动系统。

```
devcon /r classfilter DiskDrive upper +Disklog
```

在响应中，DevCon 显示 DiskDrive 类的当前筛选器驱动程序。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    Disklog
```

如果驱动程序名称拼写有误，或者尝试添加未安装在系统上的驱动程序，则该命令将失败。 除非驱动程序已注册为服务，否则 DevCon 不会添加驱动程序，也就是说，除非该驱动程序在 "服务" 注册表子项 (HKEY \_ LOCAL \_ MACHINE \\ System \\ CurrentControlSet \\ Services) 中具有子项。

以下命令测试此安全功能。 它尝试将 "Disklgg" (而不是 "Disklog" ) 添加到 DiskDrive 类的上层筛选器列表。 输出表明该命令失败。

```
devcon /r classfilter DiskDrive upper +Disklgg
devcon failed.
```

### <a name="span-idddk_example_25_insert_a_filter_driver_in_the_class_list_toolsspanspan-idddk_example_25_insert_a_filter_driver_in_the_class_list_toolsspanexample-25-insert-a-filter-driver-in-the-class-list"></a><span id="ddk_example_25_insert_a_filter_driver_in_the_class_list_tools"></span><span id="DDK_EXAMPLE_25_INSERT_A_FILTER_DRIVER_IN_THE_CLASS_LIST_TOOLS"></span><a name="ddk_example_25_insert_a_filter_driver_in_the_class_list_tools"></a>示例25：在类列表中插入筛选器驱动程序

以下命令使用 [**DevCon ClassFilter**](devcon-classfilter.md) 操作将虚构筛选器驱动程序（MyFilter.sys）添加到 DiskDrive 安装程序类的上层筛选器驱动程序列表中。 命令会在加载顺序中将 PartMgr.sys 和 Disklog.sys 之间 MyFilter.sys。

```
devcon /r classfilter DiskDrive upper @Disklog -MyFilter
```

下面的列表显示提交命令之前的 DiskDrive 类的筛选器驱动程序。

```
    PartMgr
    Disklog
```

第一个子命令 <strong>@Disklog</strong> 使用定位运算符 () 将 **@** 虚拟光标置于 Disklog 筛选器驱动程序上。 第二个子命令（ **MyFilter**）使用 "外接程序运算符" (**-**) 在 Disklog.sys 之前添加 MyFilter.sys。

该命令还使用 **/r** 参数，如果需要使类筛选器更改生效，则会重新启动系统。

在此示例中，定位运算符是必不可少的。 在 DevCon 处理任何 classfilter 子命令之前，虚拟游标位于列表的开头，并且不位于任何筛选器驱动程序上。 如果在 **+** 游标不在驱动程序上时使用 "外接程序 () " 运算符，则 DevCon 会将驱动程序添加到列表的开头。 如果在 **-** 游标不位于驱动程序上时使用 "外接程序 (") 运算符，则会将该驱动程序添加到列表的末尾。

在响应中，DevCon 显示 DiskDrive 类的当前筛选器驱动程序。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    MyFilter
    Disklog
```

你还可以使用以下命令添加 MyFilter 驱动程序并将其放置在 PartMgr 和 Disklog 之间。 在此示例中，第一个子命令将 <strong>@PartMgr</strong> 虚拟游标定位到 PartMgr 筛选器驱动程序。 第二个子命令 **+ MyFilter** 使用 "外接程序" 运算符 (+) 在 PartMgr 后添加 MyFilter.sys。

```
devcon /r classfilter DiskDrive upper @PartMgr +MyFilter
```

### <a name="span-idddk_example_26_replace_a_filter_driver_toolsspanspan-idddk_example_26_replace_a_filter_driver_toolsspanexample-26-replace-a-filter-driver"></a><span id="ddk_example_26_replace_a_filter_driver_tools"></span><span id="DDK_EXAMPLE_26_REPLACE_A_FILTER_DRIVER_TOOLS"></span><a name="ddk_example_26_replace_a_filter_driver_tools"></a>示例26：替换筛选器驱动程序

以下命令使用 [**DevCon ClassFilter**](devcon-classfilter.md) 操作将 MyFilter.sys 的原始副本替换为 DiskDrive 安装程序类的筛选器驱动程序列表中的新的和改进的 MyNewFilter.sys 版本。

```
devcon /r classfilter DiskDrive upper !MyFilter +MyNewFilter
```

下面的列表显示提交命令之前的 DiskDrive 类的筛选器驱动程序。

```
    PartMgr
    MyFilter
    Disklog
```

第一个子命令使用 delete 运算符 (**！**) 从 DiskDrive 类的上层筛选器驱动程序列表中删除 MyFilter。  (它不会影响 C： \\ Windows \\ System32 驱动程序目录中的 MyFilter.sys 文件 \\ 。 ) 

第二个子命令使用 "外接程序运算符" (**+**) 将新筛选器驱动程序置于已删除驱动程序的位置。 由于 delete 运算符将光标置于已删除的筛选器所占用的位置，因此 (**-**) 和外接 (**+**) 运算符具有相同的效果。 ) 

该命令还使用 **/r** 参数，如果需要使类筛选器更改生效，则会重新启动系统。

在响应中，DevCon 显示了 DiskDrive 类的新类筛选器配置。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    MyNewFilter
    Disklog
```

### <a name="span-idddk_example_27_change_the_order_of_filter_drivers_toolsspanspan-idddk_example_27_change_the_order_of_filter_drivers_toolsspanexample-27-change-the-order-of-filter-drivers"></a><span id="ddk_example_27_change_the_order_of_filter_drivers_tools"></span><span id="DDK_EXAMPLE_27_CHANGE_THE_ORDER_OF_FILTER_DRIVERS_TOOLS"></span><a name="ddk_example_27_change_the_order_of_filter_drivers_tools"></a>示例27：更改筛选器驱动程序的顺序

以下命令使用 [**DevCon ClassFilter**](devcon-classfilter.md) 操作来更改 DiskDrive 安装程序类的筛选器驱动程序的顺序。 具体而言，它将反转第二个和第三个筛选器驱动程序的顺序。

```
devcon /r classfilter DiskDrive upper !Disklog =@PartMgr +Disklog
```

下面的列表显示提交命令之前的 DiskDrive 类的筛选器驱动程序。 它还显示该命令的预期结果。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">以前</th>
<th align="left">完成</th>
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

 

第一个子命令使用 delete 运算符 (**！ )** 从列表中删除 Disklog。 第二个子命令使用 start 运算符 (**=)** 将虚拟光标移回起始位置，然后使用定位运算符 (**@ )** 将光标放在 PartMgr 驱动程序中。 启动运算符是必需的，因为虚拟游标仅在列表中向前移动。 最后一个子命令使用 "外接程序" 运算符 (**+)** 在 PartMgr 之后添加 Disklog。

在响应中，DevCon 显示了 DiskDrive 类的新类筛选器配置。

```
Class filters changed. Class devices must be restarted for changes to take effect.
    PartMgr
    Disklog
    MyNewFilter
```

### <a name="span-idddk_example_28_enable_a_particular_device_toolsspanspan-idddk_example_28_enable_a_particular_device_toolsspanexample-28-enable-a-particular-device"></a><span id="ddk_example_28_enable_a_particular_device_tools"></span><span id="DDK_EXAMPLE_28_ENABLE_A_PARTICULAR_DEVICE_TOOLS"></span><a name="ddk_example_28_enable_a_particular_device_tools"></a>示例28：启用特定设备

以下命令使用 [**DevCon enable**](devcon-enable.md) 操作来启用已禁用的可编程中断控制器以更正系统问题。 由于控制器硬件 ID \* PNP0000 包含一个星号，因此该命令使用单引号字符 (**"**) 指示 DevCon 准确查找在命令中指定的硬件 ID。 否则，星号将被解释为通配符。

```
devcon enable '*PNP0000
```

在响应中，DevCon 显示设备的设备实例 ID，并说明必须重新启动系统以启用设备。

```
ACPI\PNP0000\4&B4063F4&0                                    : Enabled on reboot
Not all of 1 device(s) enabled, at least one requires reboot to complete the operation.
```

可以通过以下方式进行响应：手动重启系统，或使用 [**DevCon Reboot**](devcon-reboot.md) 操作进行响应。

以下命令将 **/r** 参数添加到前一个命令。 **/R** 参数仅在需要重新启动才能完成操作时重新启动系统。

```
devcon /r enable '*PNP0000
```

在响应中，DevCon 启用设备，然后重新启动系统以使启用生效。

系统启动时，请使用 DevCon status 命令来确认设备是否已启用。

```
devcon status '*PNP0000

ACPI\PNP0000\4&B4063F4&0
    Name: Programmable interrupt controller
    Driver is running.
```

### <a name="span-idddk_example_29_enable_devices_by_class_toolsspanspan-idddk_example_29_enable_devices_by_class_toolsspanexample-29-enable-devices-by-class"></a><span id="ddk_example_29_enable_devices_by_class_tools"></span><span id="DDK_EXAMPLE_29_ENABLE_DEVICES_BY_CLASS_TOOLS"></span><a name="ddk_example_29_enable_devices_by_class_tools"></a>示例29：按类启用设备

以下命令在 [**DevCon Enable**](devcon-enable.md) 命令中指定打印机安装程序类，以启用计算机上的所有打印机设备。 该命令包括 **/r** 参数，如果需要使其生效，则会重新启动系统。

```
devcon /r enable =Printer
```

在响应中，DevCon 显示它在 Printer 类中找到的打印机的设备实例 ID，并报告已启用该 ID。 尽管该命令包含 **/r** 参数，但系统不会重新启动，因为启用打印机不需要重新启动。

```
LPTENUM\HEWLETT-PACKARDDESKJET_1120C\1&7530F08&0&LPT1.4        : Enabled
1 device(s) enabled.
```

### <a name="span-idddk_example_30_disable_devices_by_an_id_pattern_toolsspanspan-idddk_example_30_disable_devices_by_an_id_pattern_toolsspanexample-30-disable-devices-by-an-id-pattern"></a><span id="ddk_example_30_disable_devices_by_an_id_pattern_tools"></span><span id="DDK_EXAMPLE_30_DISABLE_DEVICES_BY_AN_ID_PATTERN_TOOLS"></span><a name="ddk_example_30_disable_devices_by_an_id_pattern_tools"></a>示例30：按 ID 模式禁用设备

以下命令使用 [**DevCon disable**](devcon-disable.md) 操作来禁用本地计算机上的 USB 设备。 它通过硬件 ID 模式 (USB) 来确定设备 \* 。 此模式将匹配其硬件 ID 或兼容 ID 以 "USB" 开头的任何设备。 该命令包括 **/r** 参数，如果有必要使禁用生效，则会重新启动系统。

**注意**   使用 ID 模式禁用设备之前，请确定哪些设备将受到影响。 若要执行此操作，请在显示命令中使用模式，如 **devcon STATUS \\ usb** _ 或 _*devcon hwid \\ USB* *_。

 

```
devcon /r disable USB_
```

在响应中，DevCon 显示 USB 设备的设备实例 Id，并报告它们处于禁用状态。 尽管该命令包含 **/r** 参数，但系统不会重新启动，因为禁用设备不需要重新启动。

```
USB\ROOT_HUB\4&2A40B465&0
: Disabled
USB\ROOT_HUB\4&7EFA360&0
: Disabled
USB\VID_045E&PID_0039\5&29F428A4&0&2
: Disabled
3 device(s) disabled.
```

### <a name="span-idddk_example_31_disable_devices_by_device_instance_id_toolsspanspan-idddk_example_31_disable_devices_by_device_instance_id_toolsspanexample-31-disable-devices-by-device-instance-id"></a><span id="ddk_example_31_disable_devices_by_device_instance_id_tools"></span><span id="DDK_EXAMPLE_31_DISABLE_DEVICES_BY_DEVICE_INSTANCE_ID_TOOLS"></span><a name="ddk_example_31_disable_devices_by_device_instance_id_tools"></a>示例31：按设备实例 ID 禁用设备

以下命令使用 [**DevCon disable**](devcon-disable.md) 操作来禁用本地计算机上的 USB 设备。 此命令通过其设备实例 Id （在 **@** 每个 ID 之前)  (）来标识设备。 每个设备实例 ID 通过空格与其他 ID 分隔开。

此外，因为设备实例 Id 包含与号字符 (**&**) ，所以它们用引号引起来。 该命令包括 **/r** 参数，如果有必要使禁用生效，则会重新启动系统。

```
devcon /r disable "@USB\ROOT_HUB\4&2A40B465&0" "@USB\ROOT_HUB\4&7EFA360&0" "@USB\VID_045E&PID_0039\5&29F428A4&0&2"
```

在响应中，DevCon 显示 USB 设备的设备实例 Id，并报告它们处于禁用状态。 尽管该命令包含 **/r** 参数，但系统不会重新启动，因为禁用设备不需要重新启动。

```
USB\ROOT_HUB\4&2A40B465&0
: Disabled
USB\ROOT_HUB\4&7EFA360&0
: Disabled
USB\VID_045E&PID_0039\5&29F428A4&0&2
: Disabled
3 device(s) disabled.
```

### <a name="span-idddk_example_32_update_the_driver_for_communication_ports_toolsspanspan-idddk_example_32_update_the_driver_for_communication_ports_toolsspanexample-32-update-the-driver-for-communication-ports"></a><span id="ddk_example_32_update_the_driver_for_communication_ports_tools"></span><span id="DDK_EXAMPLE_32_UPDATE_THE_DRIVER_FOR_COMMUNICATION_PORTS_TOOLS"></span><a name="ddk_example_32_update_the_driver_for_communication_ports_tools"></a>示例32：更新通信端口的驱动程序

以下命令使用 [**DevCon Update**](devcon-update.md) 操作将系统上的通信端口的当前设备驱动程序替换为在测试 .inf 文件中指定的测试驱动程序。 此命令仅影响整个硬件 ID 为 \* PNP0501 的设备 (包括星号) 。

你可以使用此命令将系统上的已签名驱动程序替换为用于测试或故障排除的备用驱动程序，或将设备与相同驱动程序的最新版本关联。

```
devcon update c:\windows\inf\test.inf *PNP0501
```

在响应中，DevCon 显示 **硬件安装** 警告，说明该驱动程序未通过 Windows 徽标测试。 如果选择对话框中的 " **继续** " 按钮，安装将继续进行。

然后，DevCon 显示以下成功消息。

```
Updating drivers for *PNP0501 from c:\windows\inf\test.inf.
Drivers updated successfully.
```

你还可以使用 [**Devcon UpdateNI**](devcon-updateni.md) 操作（ **devcon 更新** 操作的非交互式版本）更新驱动程序。 **Devcon UpdateNI** 操作与 **DevCon 更新** 操作相同，不同之处在于，它取消了需要响应的所有用户提示，并假定默认响应提示。

以下命令使用 **DevCon UpdateNI** 操作安装测试驱动程序。

```
devcon updateni c:\windows\inf\test.inf *PNP0501
```

在这种情况下，DevCon 不显示 **硬件安装** 警告。 相反，它会假定默认响应，即 **停止安装**。 因此，DevCon 无法更新驱动程序并显示失败消息。

```
Updating drivers for *PNP0501 from c:\windows\inf\test.inf.
devcon failed.
```

### <a name="span-idddk_example_33_install_a_device_toolsspanspan-idddk_example_33_install_a_device_toolsspanexample-33-install-a-device"></a><span id="ddk_example_33_install_a_device_tools"></span><span id="DDK_EXAMPLE_33_INSTALL_A_DEVICE_TOOLS"></span><a name="ddk_example_33_install_a_device_tools"></a>示例33：安装设备

以下命令使用 [**DevCon 安装**](devcon-install.md) 操作在本地计算机上安装键盘设备。 命令包含设备的 INF 文件的完整路径 () 和硬件 ID (\* PNP030b) 。

```
devcon /r install c:\windows\inf\keyboard.inf *PNP030b
```

在响应中，DevCon 报告它已安装了设备，即，它为新设备创建了一个设备节点并更新了设备的驱动程序文件。

```
Device node created. Install is complete when drivers files are updated...
Updating drivers for *PNPO30b from c:\windows\inf\keyboard.inf
Drivers updated successfully.
```

### <a name="span-idddk_example_34_install_a_device_using_unattended_setup_toolsspanspan-idddk_example_34_install_a_device_using_unattended_setup_toolsspanexample-34-install-a-device-using-unattended-setup"></a><span id="ddk_example_34_install_a_device_using_unattended_setup_tools"></span><span id="DDK_EXAMPLE_34_INSTALL_A_DEVICE_USING_UNATTENDED_SETUP_TOOLS"></span><a name="ddk_example_34_install_a_device_using_unattended_setup_tools"></a>示例34：使用无人参与安装程序安装设备

下面的示例演示如何在无人参与安装的 Microsoft Windows XP 过程中安装 Microsoft 环回适配器。

若要在无人参与的安装过程中安装此设备，请首先将以下文件添加到软盘： devcon.exe 和 netloop (C： \\ Windows \\ inf \\ netloop) 。

然后，若要添加到无人参与安装文件的 **\[ GUIRunOnce \]** 部分，请添加以下 DevCon 命令：

```
a:\devcon /r install a:\Netloop.inf '*MSLOOP
```

此命令通过使用环回适配器的硬件 ID MSLOOP 来识别它 \* 。 "MSLOOP" 前面的单引号字符 \* 告知 DevCon 按原义解释字符串，即，将星号解释为硬件 ID 的一部分，而不是通配符。

此命令还指定在安装的软盘) 上，DevCon 使用 Netloop 文件 (。 **/R** 参数仅在需要重新启动才能完成安装时重新启动计算机。

最后，将网络配置设置添加到无人参与安装文件，并运行无人参与安装。

### <a name="span-idddk_example_35_remove_devices_by_device_instance_id_pattern_toolsspanspan-idddk_example_35_remove_devices_by_device_instance_id_pattern_toolsspanexample-35-remove-devices-by-device-instance-id-pattern"></a><span id="ddk_example_35_remove_devices_by_device_instance_id_pattern_tools"></span><span id="DDK_EXAMPLE_35_REMOVE_DEVICES_BY_DEVICE_INSTANCE_ID_PATTERN_TOOLS"></span><a name="ddk_example_35_remove_devices_by_device_instance_id_pattern_tools"></a>示例35：按设备实例 ID 模式删除设备

以下命令使用 [**DevCon remove**](devcon-remove.md) 操作从计算机中删除所有 USB 设备。 它通过一个设备实例 ID 模式来标识设备，该模式与以 "USB" 字符串开头 (注册表路径) 中的任何设备实例 ID 匹配 \\ 。 At 字符 (**@**) 将设备实例 id 与硬件 id 或兼容 ID 区分开来。 此命令还包括 **/r** 参数，该参数在需要使删除过程生效时重新启动系统。

**警告**   在使用模式删除任何设备之前，确定受影响的设备。 为此，请在显示命令中使用模式，如 <strong> devcon status @usb \\ \</strong> * 或 <strong> devcon hwid @usb \\ \</strong> *。

 

```
devcon /r remove @usb\*
```

在响应中，DevCon 显示它所删除的设备的设备实例 ID。

```
USB\ROOT_HUB\4&2A40B465&0                             : Removed
USB\ROOT_HUB\4&7EFA360&0                              : Removed
USB\VID_045E&PID_0039\5&29F428A4&0&2                  : Removed
3 device(s) removed.
```

### <a name="span-idddk_example_36_remove_a_particular_network_device_toolsspanspan-idddk_example_36_remove_a_particular_network_device_toolsspanexample-36-remove-a-particular-network-device"></a><span id="ddk_example_36_remove_a_particular_network_device_tools"></span><span id="DDK_EXAMPLE_36_REMOVE_A_PARTICULAR_NETWORK_DEVICE_TOOLS"></span><a name="ddk_example_36_remove_a_particular_network_device_tools"></a>示例36：删除特定网络设备

以下命令使用 [**DevCon Remove**](devcon-remove.md) 操作从本地计算机中卸载 NDISWAN 微型端口驱动程序。 命令指定 Net 类，然后通过在类中指定设备的硬件 ID 或兼容 ID 包含 "ndiswan" 来精炼搜索。 此命令还包括 **/r** 参数，如果需要重新启动才能使删除过程生效，则会重新启动系统。

**警告**   在使用模式删除任何设备之前，请确定哪些设备将受到影响。 为此，请在显示命令中使用模式，如 **devcon status = net \* ndiswan \\*** 或 * * devcon hwid = net \* ndiswan \\ * * *。

 

```
devcon /r remove =net *ndiswan*
```

在响应中，DevCon 显示它所删除的设备的设备实例 ID。

```
ROOT\MS_NDISWANIP\0000 : Removed 1 device(s) removed.
```

### <a name="span-idddk_example_37_scan_the_computer_for_new_devices_toolsspanspan-idddk_example_37_scan_the_computer_for_new_devices_toolsspanexample-37-scan-the-computer-for-new-devices"></a><span id="ddk_example_37_scan_the_computer_for_new_devices_tools"></span><span id="DDK_EXAMPLE_37_SCAN_THE_COMPUTER_FOR_NEW_DEVICES_TOOLS"></span><a name="ddk_example_37_scan_the_computer_for_new_devices_tools"></a>示例37：扫描计算机中的新设备

以下命令使用 [**DevCon 重新扫描**](devcon-rescan.md) 操作来扫描本地计算机中的新设备。

```
devcon rescan
```

在响应中，DevCon 报告它扫描了系统，但找不到新的设备。

```
Scanning for new hardware.
Scanning completed.
```

你还可以在远程计算机上使用 **DevCon 重新扫描** 命令。 下面的命令通过将 **/m** 参数添加到命令，在 Server01 （远程计算机）上运行 **DevCon 重新扫描** 操作。

```
devcon /m:\\server01 rescan
```

### <a name="span-idddk_example_38_restart_a_device_toolsspanspan-idddk_example_38_restart_a_device_toolsspanexample-38-restart-a-device"></a><span id="ddk_example_38_restart_a_device_tools"></span><span id="DDK_EXAMPLE_38_RESTART_A_DEVICE_TOOLS"></span><a name="ddk_example_38_restart_a_device_tools"></a>示例38：重新启动设备

以下命令使用 [**DevCon restart**](devcon-restart.md) 操作来重新启动本地计算机上的回送适配器。 此命令将搜索限制为 Net setup 类，并在该类中指定环回适配器的设备实例 ID， **ROOT \\ \* MSLOOP \\ 0000**。 位于字符 (**@**) 将字符串标识为设备实例 ID。 单引号字符 (**"**) ，用于请求文本搜索，阻止 DEVCON 将 ID 中的星号解释为通配符。

```
devcon restart =net @'ROOT\*MSLOOP\0000
```

在响应中，DevCon 显示设备的设备实例 ID 并报告结果。

```
ROOT\*MSLOOP\0000                                              : Restarted
1 device(s) restarted.
```

### <a name="span-idddk_example_39_reboot_the_local_computer_toolsspanspan-idddk_example_39_reboot_the_local_computer_toolsspanexample-39-reboot-the-local-computer"></a><span id="ddk_example_39_reboot_the_local_computer_tools"></span><span id="DDK_EXAMPLE_39_REBOOT_THE_LOCAL_COMPUTER_TOOLS"></span><a name="ddk_example_39_reboot_the_local_computer_tools"></a>示例39：重新启动本地计算机

以下命令使用 [**DevCon reboot**](devcon-reboot.md) 操作来重新启动本地计算机上的操作系统，并将重新启动与硬件安装相关联。 与 **/r** 参数不同， **DevCon Reboot** 操作不依赖于其他操作的返回代码。

你可以将此命令包含在需要系统重新启动的脚本和批处理文件中。

```
devcon reboot
```

在响应中，DevCon 显示一条消息，指示它正在重新启动计算机， (重新启动本地计算机) 。


DevCon 使用标准的 **ExitWindowsEx** 函数来重新启动。 如果用户在计算机上有打开的文件，或程序不会关闭，则系统不会重新启动，直到用户响应系统提示以关闭文件或结束进程。

### <a name="span-idddk_example_40_assign_a_hardware_id_to_a_legacy_device_toolsspanspan-idddk_example_40_assign_a_hardware_id_to_a_legacy_device_toolsspanexample-40-assign-a-hardware-id-to-a-legacy-device"></a><span id="ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools"></span><span id="DDK_EXAMPLE_40_ASSIGN_A_HARDWARE_ID_TO_A_LEGACY_DEVICE_TOOLS"></span><a name="ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools"></a>示例40：向旧设备分配硬件 ID

以下命令使用 [**DevCon SetHwID**](devcon-sethwid.md) 操作将硬件 ID （嘟嘟声）分配给旧的提示音设备。

该命令使用设备的设备实例 ID，即根 \\ 旧 \_ 提示 \\ 0000，因为报警旧设备没有硬件 Id 或兼容 id。 它使用 at 字符 (**@**) 指示字符串是设备实例 ID。

此命令不使用任何符号参数来定位 ID。 默认情况下，DevCon 将新的硬件 Id 添加到硬件 ID 列表的末尾。 在这种情况下，因为设备没有其他硬件 Id，所以放置是不相关的。

```
devcon sethwid @ROOT\LEGACY_BEEP\0000 := beep
```

在响应中，DevCon 显示一条消息，指示该消息已添加到设备的硬件 ID 列表。 它还会显示生成的硬件 ID 列表。 在这种情况下，列表中只有一个硬件 ID。

```
ROOT\LEGACY_BEEP\0000                              : beep
Modified 1 hardware ID(s).
```

### <a name="span-idddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_comspanspan-idddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_comspanexample-41-add-a-hardware-id-to-all-legacy-devices-on-a-remote-computer"></a><span id="ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com"></span><span id="DDK_EXAMPLE_41_ADD_A_HARDWARE_ID_TO_ALL_LEGACY_DEVICES_ON_A_REMOTE_COM"></span><a name="ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com"></a>示例41：向远程计算机上的所有旧设备添加硬件 ID

以下命令使用 [**DevCon SetHwID**](devcon-sethwid.md) 操作将硬件 id （旧）添加到 Server1 远程计算机上所有旧式设备的硬件 id 列表。

此命令使用 **-** 符号参数将新的硬件 id 添加到设备的硬件 id 列表的末尾，以防为某个设备创建了首选硬件 id。 它使用 **/m** 参数来指定远程计算机。 它还使用旧的设备实例 id 模式 <strong> @ROOT \\ \</strong> <em>来识别计算机上的旧设备，即，其设备实例 id 以 **ROOT \\ 旧版本</em>开头的所有设备*。

```
devcon /m:\\Server1 sethwid @ROOT\LEGACY* := -legacy
```

在响应中，DevCon 显示所有受影响设备的结果硬件 ID 列表。

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

将相同的硬件 ID 分配给一组设备后，可以使用其他 DevCon 操作在单个命令中查看和更改设备。

例如，以下命令显示所有旧设备的状态。

```
devcon status legacy
```

### <a name="span-idddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remotspanspan-idddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remotspanexample-42-delete-a-hardware-id-from-all-legacy-devices-on-a-remote-computer"></a><span id="ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot"></span><span id="DDK_EXAMPLE_42_DELETE_A_HARDWARE_ID_FROM_ALL_LEGACY_DEVICES_ON_A_REMOT"></span><a name="ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot"></a>示例42：从远程计算机上的所有旧设备中删除硬件 ID

以下命令使用 [**DevCon SetHwID**](devcon-sethwid.md) 操作从 Server1 远程计算机上所有旧设备的硬件 id 列表中删除 **旧** 的硬件 id。

该命令使用 **/m** 参数来指定远程计算机。 它使用 **旧** 硬件 id 来标识具有该硬件 id 的所有设备。 然后，它使用 **！** 用于删除 **旧** 硬件 ID 的符号参数。

```
devcon /m:\\Server1 sethwid legacy := !legacy
```

在响应中，DevCon 显示所有受影响设备的结果硬件 ID 列表。

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

### <a name="span-idddk_example_43_add_delete_and_replace_hardwareids_toolsspanspan-idddk_example_43_add_delete_and_replace_hardwareids_toolsspanexample-43-add-delete-and-replace-hardware-ids"></a><span id="ddk_example_43_add_delete_and_replace_hardwareids_tools"></span><span id="DDK_EXAMPLE_43_ADD_DELETE_AND_REPLACE_HARDWAREIDS_TOOLS"></span><a name="ddk_example_43_add_delete_and_replace_hardwareids_tools"></a>示例43：添加、删除和替换硬件 Id

下面的示例演示如何使用 [**DevCon SetHwID**](devcon-sethwid.md) 操作的各种功能。

此系列使用虚拟设备 DeviceX，其中包含设备实例 ID， **根 \\ DeviceX \\ 0000**。 使用 DevCon 之前，设备具有以下硬件 Id 列表：

```
Hw3 Hw4
```

以下命令使用 **+** 符号将 **Hw1** 和 **Hw2** 添加到 DeviceX 硬件 id 列表的开头。 由于 **Hw2** 已显示在列表中，因此它将被移动，而不会添加。 命令通过其设备实例 ID 来标识设备，如 ID 前面的字符 () 所示 **@** 。

```
devcon sethwid @ROOT\DEVICEX\0000 := +Hw1 Hw2
```

在响应中，DevCon 显示设备的新硬件 ID 列表。 请注意， **Hw1** 和 **Hw2** 按指定顺序出现在列表的开头。

```
ROOT\DEVICEX\0000                         : Hw1,Hw2,Hw3,Hw4
Modified 1 hardware ID(s).
```

此外，DevCon 报告它修改了一个硬件 ID 列表，即一个设备的硬件 ID 列表。

以下命令使用 **！** 用于删除 **Hw1** 硬件 ID 的符号。 然后，它会列出不带符号参数的硬件 ID **Hw5**。 如果没有符号参数，SetHwID 会将硬件 ID 添加到设备的硬件 ID 列表的末尾。

此命令表明，与 **DevCon SetHwID** 操作的其他符号参数不同， **！** 符号仅适用于其前缀的硬件 ID。

```
devcon sethwid @ROOT\DeviceX\0000 := !Hw1 Hw5
```

在响应中，DevCon 显示 DeviceX 的结果硬件 ID 列表。

```
ROOT\DEVICEX\0000                         : Hw2,Hw3,Hw4,Hw5
Modified 1 hardware ID(s).
```

以下命令使用 = 参数将 DeviceX 列表中的所有硬件 id 替换为单个硬件 ID **DevX**。

```
devcon sethwid @ROOT\DeviceX\0000 := =DevX
```

在响应中，DevCon 显示 DeviceX 的结果硬件 ID 列表。

```
ROOT\DEVICEX\0000                         : DevX
Modified 1 hardware ID(s).
```

成功消息指示 DevCon 修改了一个设备的硬件 ID。

### <a name="span-idddk_example_44_forcibly_update_the_hal_toolsspanspan-idddk_example_44_forcibly_update_the_hal_toolsspanexample-44-forcibly-update-the-hal"></a><span id="ddk_example_44_forcibly_update_the_hal_tools"></span><span id="DDK_EXAMPLE_44_FORCIBLY_UPDATE_THE_HAL_TOOLS"></span><a name="ddk_example_44_forcibly_update_the_hal_tools"></a>示例44：强制更新 HAL

下面的示例演示如何使用 DevCon 更新计算机上的 HAL。 在此示例中，测试人员需要将最适合于具有多处理器 APCI APIC HAL 的计算机的单处理器 APCI APIC HAL 替换为测试目的。

第一个命令使用 [**DevCon SetHwID**](devcon-sethwid.md)操作将 HAL 的硬件 id 从 acpiapic （即，单处理器 hal 的硬件 id）更改为 **acpiapic \_ Mp**（多处理器 hal 的硬件 id）。 **\_**

必须更改硬件 ID，因为 HAL 的 INF 文件包含用于单处理器和多处理器 Hal 的驱动程序。 系统根据设备的硬件 ID 从 INF 文件中选择最适合的驱动程序。 如果不更改硬件 ID，则 **DevCon Update** 命令只需重新安装单处理器 HAL 驱动程序。

在下面的命令中，该命令通过 ID 前面的字符所指示的实例 ID （ **根 \\ ACPI \_ HAL \\ 0000**）来标识 HAL **@** 。 该命令使用 **+** 字符使 **acpiapic \_ mp** 成为 HAL 列表中的第一个硬件 ID。 然后，它使用 **！** 要从 HAL 的 Id 列表中删除 **acpiapic \_** 的硬件 ID 的字符。

```
devcon sethwid @ROOT\ACPI_HAL\0000 := +acpiapic_mp !acpiapic_up
```

在响应中，DevCon 为 HAL 显示以下新的硬件 ID 列表。

```
ROOT\ACPI_HAL\0000                         : acpiapic_mp
Modified 1 hardware ID(s).
```

以下命令使用 [**DevCon 更新**](devcon-update.md) 操作来更新 HAL 的驱动程序。

```
devcon update c:\windows\inf\hal.inf acpiapic_mp
```

然后，DevCon 显示以下成功消息。

```
Updating drivers for acpiapic_mp from c:\windows\inf\hal.inf.
Drivers updated successfully.
```

 

 





