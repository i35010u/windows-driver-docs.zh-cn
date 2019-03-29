---
title: 识别内部相机的位置
description: 本主题提供有关在 Windows 8.1 中的系统上支持内部相机的信息。
ms.assetid: 7664F0F6-BD95-4919-82E4-F6F8080C2B5B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af9bc003e24c90fa776d8161af8879e8ca9d1fc6
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463959"
---
# <a name="identifying-the-location-of-internal-cameras-uwp-device-apps"></a>确定内部相机 （UWP 设备应用） 的位置


本主题提供有关在 Windows 8.1 中的系统上支持内部相机的信息。 它介绍了如何识别的内置相机物理位置，以便它们能够正常运行的 UWP 应用。 它还介绍了如何设置模型 ID，以使照相机适用于 UWP 的设备应用程序。 若要在一般情况下了解有关 UWP 的设备应用程序的详细信息，请参阅[满足 UWP 设备应用](meet-uwp-device-apps.md)。

## <a name="span-idprovidingphysicallocationspanspan-idprovidingphysicallocationspanspan-idprovidingphysicallocationspanproviding-physical-location"></a><span id="Providing_physical_location"></span><span id="providing_physical_location"></span><span id="PROVIDING_PHYSICAL_LOCATION"></span>提供物理位置


从表面上讲固定方向的内置相机的系统必须报告相机的物理位置。 此物理位置信息指示的方向面向照相机，如前面或后面，以便在 Windows 8.1 中使用相机应用正常工作。

以下两个[Windows 硬件认证要求](https://go.microsoft.com/fwlink/p/?LinkId=320504)，它允许 Windows 识别照相机的位置，则需要：

-   **System.Client.PCContainer.PCAppearsAsSingleObject**。 照相机必须分组到计算机的设备容器，其中包含以物理方式位于计算机内的设备函数。 必须将相机分组到计算机的设备容器中公开到应用，其物理位置，是因为外部的计算机容器的设备不假定有机械地固定的方向。

-   **System.Client.Webcam.PhysicalLocation**。 固件必须通过使用提供的物理位置信息\_以前 ACPI 表，以指示的位置和方向的照相机中的信息。

### <a name="span-idwhydoeswindowsneedthephysicallocationcamerasspanspan-idwhydoeswindowsneedthephysicallocationcamerasspanspan-idwhydoeswindowsneedthephysicallocationcamerasspanwhy-does-windows-need-the-physical-location-cameras"></a><span id="Why_does_Windows_need_the_physical_location_cameras_"></span><span id="why_does_windows_need_the_physical_location_cameras_"></span><span id="WHY_DOES_WINDOWS_NEED_THE_PHYSICAL_LOCATION_CAMERAS_"></span>为什么 Windows 需要的物理位置相机？

Windows 需要能够确定内部相机的物理位置，原因如下：

-   UWP 应用使用的物理位置来确定哪个相机，以使用多个相机是否存在。 例如，一个聊天应用程序将默认为使用应用程序启动时的人脸用户前摄像头。
-   UWP 应用使用的物理位置来确定如何镜像或旋转视频预览。
-   如果照相机是用户，请在预览应看起来像用户查找到镜像。 若要执行此操作，该应用程序将翻转的左侧和右侧的预览，以便在预览映射视频。 如果照相机背用户，则不需要镜像视频应用程序。
-   如果应用程序将旋转预览，旋转的度数而异的照相机的位置。

### <a name="span-idhowtogroupthecameraintothecomputersdevicecontainerspanspan-idhowtogroupthecameraintothecomputersdevicecontainerspanspan-idhowtogroupthecameraintothecomputersdevicecontainerspanhow-to-group-the-camera-into-the-computers-device-container"></a><span id="How_to_group_the_camera_into_the_computers_device_container"></span><span id="how_to_group_the_camera_into_the_computers_device_container"></span><span id="HOW_TO_GROUP_THE_CAMERA_INTO_THE_COMPUTERS_DEVICE_CONTAINER"></span>如何将相机分组到计算机的设备容器

根据认证要求**System.Client.PCContainer.PCAppearsAsSingleObject**，也称为 SYSFUND 0200，内部相机的设备节点必须归入 PC 设备容器。 换而言之，内部照相机应不会显示在**设备和打印机**和必须合并到 PC 容器。

若要实现这一要求的方式取决于内部相机的总线类型。 如果设备可以公开在 ACPI 表中的物理设备位置的信息，可以通过包含指定 ACPI 层中的正确分组\_以前中的表和修改在 ACPI 表中，UserVisible 标志，如中所述的信息[多功能设备支持和设备容器分组](https://go.microsoft.com/fwlink/p/?LinkId=320505)。 否则，使用重写 removable 标志 DeviceOverrides 注册表项。 有关详细信息，请参阅[DeviceOverrides 注册表项](https://go.microsoft.com/fwlink/p/?LinkId=320506)。

### <a name="span-idhowtoprovidephysicallocationusingpldinfointheacpitablespanspan-idhowtoprovidephysicallocationusingpldinfointheacpitablespanspan-idhowtoprovidephysicallocationusingpldinfointheacpitablespanhow-to-provide-physical-location-using-pld-info-in-the-acpi-table"></a><span id="How_to_provide_physical_location_using__PLD_info_in_the_ACPI_table"></span><span id="how_to_provide_physical_location_using__pld_info_in_the_acpi_table"></span><span id="HOW_TO_PROVIDE_PHYSICAL_LOCATION_USING__PLD_INFO_IN_THE_ACPI_TABLE"></span>如何提供物理位置使用\_以前 ACPI 表中的信息

根据认证要求**System.Client.Webcam.PhysicalLocation**，则\_ACPI （高级配置和电源接口中必须提供以前值，该值指示照相机的位置) 表。 这适用于任何照相机设备内置的系统底盘且具有机械地修复方向。 固件必须提供\_以前方法并设置面板字段 (bits\[69:67\]) 为在其装载照相机的面板的相应值。 例如，前端表示照相机面临用户 （网络摄像机） 后，则表示照相机面临离最终用户 （仍或视频摄像机）。

| 位的值\[69:67\] | 面板   |
|-------------------------|---------|
| 0                       | 顶部     |
| 1                       | 底部  |
| 2                       | 向左    |
| 3                       | 向右   |
| 4                       | 前端   |
| 5                       | 后退    |
| 6                       | Unknown |

 

此外，位 143:128 （垂直偏移量），并且位 159:144 （水平偏移量） 必须提供与显示相机的相对位置。 此原点相对于显示组件中的本机像素寻址，并且应与匹配的横向或纵向显示的显示方向。 源是显示的左下角，其中正水平滚动条和垂直偏移量值向右、 向上，分别为。

对于连接了 USB 的内部相机、 USB 设备的设备节点将创建在 USB 端口设备节点下的 ACPI 表中。

若要指定的地址 (\_ADR)，请执行以下步骤。

1.  将 Windows 安装到目标 PC
2.  转到**设备管理器**
3.  右键单击目标 webacm 并选择**属性**
4.  打开**详细信息**选项卡并选择**地址**中**属性**菜单
5.  中的值**值**框是位于你的设备的地址
6.  中的值设置\_ACPI 表中的 ADR
7.  设置\_以前值基于 ACPI 规范和 PC 设计

此示例是用于连接了 USB 的照相机的 ACPI 表。 在此示例中，值为 0x1。 第九个字节包含位置的面板代码 (bits\[69:67\])。 请注意，是否设备是 USB 复合设备，以前必须是对视频的函数。 这意味着将所需的附加 Device() 条目。

```Text
Device(PRTD)
{
     Name(_ADR, 0x6)
     Name(_UPC, Package(0x4)
     {
            ....
     }
     Name(_PLD, Buffer(0x10)
     {
            ....
     }
     Device(WCAM)
     {
           Name(_ADR, 0x6)
           Name(_PLD, Buffer(0x10) {
           0x81, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
           0x20, 0x1C, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00})
     }
}
```

有关更多详细信息，请参阅 ACPI 规范\_以前。

对于 USBCCGP 的下游节点，通过将端口号添加到第一个接口数字照相机函数的计算的地址值。 如果设备还没有加载 USBCCGP，该地址是只需的端口号。 如果你需要预测的地址号码，而无需安装 Windows，请使用以下公式来计算它。 如果目标设备是单个函数设备 （不使用 USB 复合风格的设备），使用仅端口数计算的地址值。

## <a name="span-idprovidingmodelidspanspan-idprovidingmodelidspanspan-idprovidingmodelidspanproviding-model-id"></a><span id="Providing_Model_ID"></span><span id="providing_model_id"></span><span id="PROVIDING_MODEL_ID"></span>提供模型 ID


Windows 设备元数据系统便可以查询用于在内部嵌入的相机的设备元数据包，仅当照相机的设备节点具有**模型 ID**属性和设备类别是`Imaging.Webcam`。 若要使内部相机的元数据可检测到的 Windows，以便正确与设备和应用特定于照相机的 UWP 设备应用程序相关联的设备元数据包，OEM 必须执行以下操作：

-   设置**模型 ID**在设备节点中，通过使用`InternalDeviceModification`设备注册表项中的标志

### <a name="span-idhowtosetthemodelidfortheinternalcamerasdevicenodespanspan-idhowtosetthemodelidfortheinternalcamerasdevicenodespanspan-idhowtosetthemodelidfortheinternalcamerasdevicenodespanhow-to-set-the-model-id-for-the-internal-cameras-device-node"></a><span id="How_to_set_the_Model_ID_for_the_internal_camera_s_device_node"></span><span id="how_to_set_the_model_id_for_the_internal_camera_s_device_node"></span><span id="HOW_TO_SET_THE_MODEL_ID_FOR_THE_INTERNAL_CAMERA_S_DEVICE_NODE"></span>如何设置内部相机的设备节点的模型 ID

内部相机的 OEM 创建要用于模型 ID 的 GUID，并为其创建注册表项。 **模型 ID**属性添加到设备节点上，通过使用 InternalDeviceModification 机制，它是基于注册表的查找表 (LUT) 将映射到特定设备的注册表项组成。 此 InternalDeviceModification 表维护以下注册表项下：

-   `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\InternalDeviceModification`

要在 InternalDeviceModification 注册表项下创建的子项的项是 ModelID 的 OEM 提供 GUID。 此项的状态将模型 ID 添加到相机的设备节点中，根据设备硬件 ID 和所指示的位置信息\_ACPI 表中的以前值。

![注册表项和 internaldevicemodification 的值](images/372985-camera-internal-registry-layout.png)

### <a name="span-idinternaldevicemodificationregistrykeyspanspan-idinternaldevicemodificationregistrykeyspanspan-idinternaldevicemodificationregistrykeyspaninternaldevicemodification-registry-key"></a><span id="InternalDeviceModification_registry_key"></span><span id="internaldevicemodification_registry_key"></span><span id="INTERNALDEVICEMODIFICATION_REGISTRY_KEY"></span>InternalDeviceModification 注册表项

InternalDeviceModification 注册表项指示该至少一个照相机使用 ModelID。

|                     |                                                                                  |
|---------------------|----------------------------------------------------------------------------------|
| 注册表项名称   | `InternalDeviceModification`                                                     |
| 必需/可选   | 必需                                                                         |
| 路径                | `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control`                            |
| 格式要求 | 无                                                                             |
| 有效的子项       | 模型 ID 注册表项 （请参阅以下子项格式要求和 examles） |

 

### <a name="span-idmodelidregistrykeyspanspan-idmodelidregistrykeyspanspan-idmodelidregistrykeyspanmodel-id-registry-key"></a><span id="Model_ID_registry_key"></span><span id="model_id_registry_key"></span><span id="MODEL_ID_REGISTRY_KEY"></span>模型 ID 注册表项

|                     |                                                                                            |
|---------------------|--------------------------------------------------------------------------------------------|
| 注册表项名称   | 模型 ID （确切的型号 ID 值是键名称）                                            |
| 必需/可选   | 必需                                                                                   |
| 格式要求 | 密钥名称是由 OEM 创建的 GUID。 它必须具有左、 右括号。 |
| 有效值        | 硬件 ID 注册表值或 `PLD_Panel`                                                 |
| 示例            | `{43922620-DAD9-4C05-BE3F-F65B089D84D8}`                                                   |

 

### <a name="span-idhardwareidregistryvaluespanspan-idhardwareidregistryvaluespanspan-idhardwareidregistryvaluespanhardware-id-registry-value"></a><span id="Hardware_ID_registry_value"></span><span id="hardware_id_registry_value"></span><span id="HARDWARE_ID_REGISTRY_VALUE"></span>硬件 ID 注册表值

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">注册表值名称</td>
<td align="left">HardwareIDs</td>
</tr>
<tr class="even">
<td align="left">必需/可选</td>
<td align="left">必需</td>
</tr>
<tr class="odd">
<td align="left">在任务栏的搜索框中键入</td>
<td align="left">多字符串</td>
</tr>
<tr class="even">
<td align="left">格式要求</td>
<td align="left">必须包含总线前缀的硬件 id。 所有"&amp;q u o t;字符必须替换为"#"。</td>
</tr>
<tr class="odd">
<td align="left">示例</td>
<td align="left"><p><code>USB#VID_1234&amp;PID_ABCD&amp;REV_0001</code></p>
<p><code>PCI#VEN_ABCD&amp;DEV_1234&amp;SUBSYS_000</code></p></td>
</tr>
<tr class="even">
<td align="left">备注</td>
<td align="left">可以提供多个硬件 ID 值。 系统时任何硬件 Id 列表中出现多次，设置基于硬件 ID 的设备节点的模型 ID</td>
</tr>
</tbody>
</table>

 

### <a name="span-idpldpanelregistryvaluespanspan-idpldpanelregistryvaluespanspan-idpldpanelregistryvaluespanpldpanel-registry-value"></a><span id="PLD_Panel_registry_value"></span><span id="pld_panel_registry_value"></span><span id="PLD_PANEL_REGISTRY_VALUE"></span>以前\_面板注册表值

|                     |                                                                                                  |
|---------------------|--------------------------------------------------------------------------------------------------|
| 注册表值名称 | `PLD_Panel`                                                                                      |
| 必需/可选   | 可选                                                                                         |
| 在任务栏的搜索框中键入                | DWORD                                                                                            |
| 格式要求 | 必须包括硬件 Id 的总线前缀。 所有"\\"字符必须替换为"\#"。 |
| 示例            | 4,5                                                                                              |

 

### <a name="span-idpldpaneldetailsspanspan-idpldpaneldetailsspanspan-idpldpaneldetailsspanpldpanel-details"></a><span id="PLD_Panel_Details"></span><span id="pld_panel_details"></span><span id="PLD_PANEL_DETAILS"></span>以前\_面板的详细信息

以前\_面板 ACPI 表中提供的值，将启用照相机以一个系统有两个完全相同的摄像机设备并且都具有相同的硬件 Id 时，会从每个其他可分辨。 若要创建不同的模型 Id、 硬件 Id 的组合和以前\_使用面板值。

**请注意**  以前\_面板设置注册表项中的是可选的。 Windows 将确定通过 ACPI 表中的设置的照相机的物理位置。

 

以前\_面板中的注册表值定义为\_ACPI 规范中的以前 （物理设备的位置）。 此值，该值指示其存储模块中的照相机的物理位置，必须是以下值之一。

| 值 | Description                                                         |
|-------|---------------------------------------------------------------------|
| 0     | 顶部                                                                 |
| 1     | 底部                                                              |
| 2     | 向左                                                                |
| 3     | 向右                                                               |
| 4     | 前端                                                               |
| 5     | 后退                                                                |
| 6     | 未知 （垂直位置和水平位置将被忽略） |

 

### <a name="span-idinternaldevicemodificationregistrykeyexamplesspanspan-idinternaldevicemodificationregistrykeyexamplesspanspan-idinternaldevicemodificationregistrykeyexamplesspaninternaldevicemodification-registry-key-examples"></a><span id="InternalDeviceModification_registry_key_examples"></span><span id="internaldevicemodification_registry_key_examples"></span><span id="INTERNALDEVICEMODIFICATION_REGISTRY_KEY_EXAMPLES"></span>InternalDeviceModification 注册表项示例

下面的示例演示 InternalDeviceModification 注册表项的格式。

```Text
{00001111-2222-3333-4444-555566667777} 
      HardwareIDs (Multi sz) = 
      “USB#VID_1234&PID_ABCD&REV_0001”,“USB#VID_1234&PID_ABCD"
      PLD_Panel (DWORD) = 4
{88889999-aaaa-bbbb-cccc-ddddeeeeffff} 
      HardwareIDs (multi sz) = “USB#VID_5678&PID_WXYZ&REV_0001”
      PLD_Panel (DWORD) = 5        
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\InternalDeviceModification]

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\InternalDeviceModification\{BBBF38D6-9866-493D-B86F-986E339E096D}]
"PLD_Panel"=dword:00000004
"HardwareIDs"=hex(7):55,00,53,00,42,00,23,00,56,00,49,00,44,00,5f,00,30,00,34,\
  00,35,00,45,00,26,00,50,00,49,00,44,00,5f,00,30,00,30,00,31,00,30,00,23,00,\
  52,00,45,00,56,00,5f,00,30,00,30,00,30,00,31,00,00,00,55,00,53,00,42,00,23,\
  00,56,00,49,00,44,00,5f,00,30,00,34,00,35,00,45,00,26,00,50,00,49,00,44,00,\
  5f,00,30,00,30,00,31,00,30,00,00,00,00,00
```

### <a name="span-idmetadatastructurespanspan-idmetadatastructurespanspan-idmetadatastructurespanmetadata-structure"></a><span id="Metadata_structure"></span><span id="metadata_structure"></span><span id="METADATA_STRUCTURE"></span>元数据结构

内部相机的设备元数据包的任何其他设备，设备元数据包的结构相同。 在 MetadataKey **packageinfo.xml**包内的设备元数据是使用 InternalDeviceModification 注册表项定义的模型 ID。 Windows 元数据系统下载设备元数据包基于模型的 id。 不使用内部相机的硬件 ID。

有关创建 UWP 设备应用的设备元数据的详细信息，请参阅[构建 UWP 设备应用](the-workflow.md)。

### <a name="span-idpre-installationspanspan-idpre-installationspanspan-idpre-installationspanpre-installation"></a><span id="Pre-installation"></span><span id="pre-installation"></span><span id="PRE-INSTALLATION"></span>预安装

在使用 OEM 预安装工具包 (OPK) 的设备上的 Microsoft Store 设备应用和设备元数据包可以是预装。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[适用于内部设备的 UWP 设备应用](uwp-device-apps-for-specialized-devices.md)

 

 






