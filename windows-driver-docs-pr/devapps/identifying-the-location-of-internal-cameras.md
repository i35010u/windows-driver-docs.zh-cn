---
title: 识别内部相机的位置
description: 本主题提供有关在 Windows 8.1 中的系统上支持内部相机的信息。
ms.assetid: 7664F0F6-BD95-4919-82E4-F6F8080C2B5B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b3b5a5ed0d9639fb4a4447ae39775012b68f87c
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733210"
---
# <a name="identifying-the-location-of-internal-cameras-uwp-device-apps"></a>确定 (UWP 设备应用的内部照相机位置) 

本主题提供有关在 Windows 8.1 中的系统上支持内部相机的信息。 它介绍如何识别内置相机的物理位置，使其能够正常使用 UWP 应用。 它还介绍了如何设置模型 ID，以便相机与 UWP 设备应用程序一起工作。 若要详细了解 UWP 设备应用的详细信息，请参阅了解 [uwp 设备应用](meet-uwp-device-apps.md)。

## <a name="providing-physical-location"></a>提供物理位置

具有内置相机且按机械固定方向的系统必须报告照相机的物理位置。 此物理位置信息指示相机的方向（例如正面或背面），以便在 Windows 8.1 的应用程序中使用相机。

以下两个 [Windows 硬件认证要求](/previous-versions/windows/hardware/cert-program/)（允许 Windows 识别相机位置）是必需的：

- **PCContainer. PCAppearsAsSingleObject**。 必须将照相机分组到计算机的设备容器中，该容器包含计算机上物理位置的设备功能。 必须将相机分组到计算机的设备容器中，才能向应用公开其物理位置，因为计算机容器外部的设备不会采用按机械方式固定的方向。

- " **PhysicalLocation**"。 固件必须提供物理位置信息，方法是使用 \_ ACPI 表中的 PLD 信息指明照相机的位置和方向。

### <a name="why-windows-requires-the-physical-location-cameras"></a>为什么 Windows 需要物理位置照相机

由于以下原因，Windows 需要知道内部相机的物理位置：

- UWP 应用使用物理位置来确定如果有多个相机，要使用哪种相机。 例如，在应用启动时，聊天应用程序将默认使用正面照相机来面对用户。
- UWP 应用使用物理位置确定如何镜像或旋转视频预览。
- 如果相机面向用户，则预览应类似于用户正在查看镜像。 若要执行此操作，应用将翻转预览的左侧和右侧，使预览能镜像视频。 如果相机远离用户，则应用不需要镜像视频。
- 如果应用旋转预览，旋转度会根据相机位置的不同而不同。

### <a name="how-to-group-the-camera-into-the-computers-device-container"></a>如何将照相机分组到计算机设备容器

根据证书要求 **PCContainer PCAppearsAsSingleObject**（也称为 SYSFUND-0200），必须将内部照相机设备节点组合到 PC 设备容器下。 换句话说，内部照相机不应显示在 **设备和打印机** 中，必须合并到 PC 容器。

实现此要求的方式取决于内部照相机的总线类型。 如果设备可以在 ACPI 表中显示有关物理设备位置的信息，则可以通过在 acpi 层中包含 \_ PLD 信息并修改 acpi 表中的 UserVisible 标志来指定正确的分组，如 [多功能设备支持和设备容器分组](../install/container-ids.md)中所述。 否则，请使用 DeviceOverrides 注册表项替代可移动标志。 有关详细信息，请参阅 [DeviceOverrides 注册表项](../install/deviceoverrides-registry-key.md)。

### <a name="how-to-provide-physical-location-using-_pld-info-in-the-acpi-table"></a>如何 \_ 在 ACPI 表中使用 PLD 信息提供物理位置

根据证书要求 **PhysicalLocation**， \_ PLD 值（指示照相机的位置）必须在 ACPI (高级配置和电源接口) 表中提供。 这适用于系统机箱中内置的任何照相机设备，并且具有按机械方向固定的方向。 固件必须提供 \_ PLD 方法，并将 "面板" 字段 (bits \[ 69:67 \]) 设置为装入照相机的面板的相应值。 例如，"前" 表示相机面临用户 (网络摄像机) ，而背面表明照相机远离最终用户 (仍然或视频相机) 。

| Bits 69:67 的值 \[\] | Panel   |
|-------------------------|---------|
| 0                       | TOP     |
| 1                       | 下  |
| 2                       | Left    |
| 3                       | Right   |
| 4                       | Front   |
| 5                       | Back    |
| 6                       | Unknown |

此外，位 143:128 (垂直偏移) 和 bits 159:144 (水平偏移) 必须提供与显示器相关的相机相对位置。 此原点相对于显示组件中的本机像素寻址，并且应与横向或纵向的当前显示方向匹配。 原点是显示的左下角，其中，正水平和垂直偏移值分别向右和向上偏移。

对于连接了 USB 的内置照相机，将在 USB 端口设备节点下的 ACPI 表中创建 USB 设备的设备节点。

若要指定 (ADR 的地址 \_) ：

1. 将 Windows 安装到目标 PC
2. 中转到 **设备管理器**
3. 选择并按住 (或右键单击目标网络摄像机) ，然后选择 "**属性**"
4. 打开 "**详细信息**" 选项卡，然后在**属性**菜单中选择 "**地址**"
5. " **值** " 框中的值是你的设备所在的地址
6. 在 \_ ACPI 表的 ADR 中设置值
7. \_基于 ACPI 规范和 PC 设计设置 PLD 值

此示例是连接了 USB 的照相机的 ACPI 表。 在此示例中，值为0x1。 第九个字节包含位置 (bits 69:67) 位置的面板代码 \[ \] 。 请注意，如果设备是 USB 复合设备，则 PLD 必须位于视频函数上。 这意味着需要额外的设备 ( # A1 条目。

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

有关 PLD 的更多详细信息，请参阅 ACPI 规范 \_ 。

对于 USBCCGP 的下游节点，通过将端口号添加到相机函数的第一个接口号来计算地址值。 如果没有为设备加载 USBCCGP，则该地址只是端口号。 如果需要在不安装 Windows 的情况下预测地址号，请使用此公式进行计算。 如果目标设备是单一功能设备 (不使用 USB 复合样式设备) ，则仅使用端口号计算地址值。

## <a name="providing-model-id"></a>提供模型 ID

只有照相机的设备节点具有 **型号 ID** 属性并且设备类别为，Windows 设备元数据系统才能查询内部嵌入的相机的设备元数据包 `Imaging.Webcam` 。 若要使内置相机的元数据可由 Windows 发现，以便设备元数据包正确地与设备和相机特定的 UWP 设备应用相关联，OEM 需要执行以下操作：

- 使用设备注册表项中的标志在设备节点中设置**模型 ID** `InternalDeviceModification`

### <a name="how-to-set-the-model-id-for-the-internal-cameras-device-node"></a>如何设置内部照相机设备节点的型号 ID

对于内部相机，OEM 创建用于模型 ID 的 GUID，并为其创建一个注册表项。 **模型 ID**属性是使用 InternalDeviceModification 机制添加到设备节点的，后者是基于注册表的查找表 (LUT) ，它包含映射到特定设备的注册表项。 此 InternalDeviceModification 表将保留在以下注册表项下：

- `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\InternalDeviceModification`

要在 InternalDeviceModification 注册表项下创建的子项项是 OEM 为 ModelID 提供的 GUID。 此密钥的存在会根据设备硬件 ID 和由 \_ ACPI 表中的 PLD 值指示的位置信息，将模型 ID 添加到照相机的设备节点。

![internaldevicemodification 的注册表项和值](images/372985-camera-internal-registry-layout.png)

### <a name="internaldevicemodification-registry-key"></a>InternalDeviceModification 注册表项

InternalDeviceModification 注册表项指示至少有一个相机使用 ModelID。

|注册表项名称|InternalDeviceModification|
|----|----|
|必需/可选| 必须|
|`Path`|`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control`|
|格式要求|无|
|有效子项|模型 ID 注册表项 (参阅以下子项格式要求和示例) |

### <a name="model-id-registry-key"></a>模型 ID 注册表项

| 注册表项名称   | 模型 ID (准确的模型 ID 值为密钥名称) |
|----|----|
|必需/可选|必须|
|格式要求|密钥名称是 OEM 创建的 GUID。 它必须同时具有左括号和右括号。 |
|有效值|硬件 ID 注册表值或 `PLD_Panel`|
| 示例|`{43922620-DAD9-4C05-BE3F-F65B089D84D8}`|

### <a name="hardware-id-registry-value"></a>硬件 ID 注册表值

|注册表值名称|HardwareIDs|
|----|----|
|必需/可选|必须|
|类型|多字符串|
|格式要求|必须包含硬件 ID 的总线前缀。 所有 "" 字符都必须替换为 "#"。|
|示例|`USB#VID_1234&PID_ABCD&REV_0001` <br/>`PCI#VEN_ABCD&DEV_1234&SUBSYS_000`|
|评论|可以提供多个硬件 ID 值。 当列表中的任何硬件 Id 超过一次时，系统会根据硬件 ID 设置设备节点的模型 ID。|

### <a name="pld_panel-registry-value"></a>PLD \_ 面板注册表值

| 注册表值名称 | `PLD_Panel`|
|----|----|
| 必需/可选   | 可选|
| 类型| DWORD|
| 格式要求 | 必须包含 HardwareID 的总线前缀。 所有 " \\ " 字符都必须替换为 " \# "。 |
| 示例            | 4,5|

### <a name="pld_panel-details"></a>PLD \_ 面板详细信息

\_当系统具有两个相同的相机设备并且两者都具有相同的硬件 id 时，ACPI 表中提供的 PLD 面板值使每个照相机彼此之间相互区分。 若要创建不同的模型 Id，请使用硬件 Id 和 PLD \_ 面板值的组合。

**注意**   \_注册表项中的 PLD 面板设置是可选的。 Windows 根据 ACPI 表中的设置来确定相机的物理位置。

在 \_ ACPI 规范中，PLD 面板注册表值定义为 \_ PLD (物理设备位置) 。 此值指示照相机在其机箱中的物理位置，必须是以下各项之一。

| 值 | 说明|
|-------|----------|
| 0     | TOP|
| 1     | 下|
| 2     | Left|
| 3     | Right|
| 4     | Front|
| 5     | Back |
| 6     | 将忽略未知的 (垂直位置和水平位置)  |

### <a name="internaldevicemodification-registry-key-examples"></a>InternalDeviceModification 注册表项示例

以下示例演示了 InternalDeviceModification 注册表项的格式。

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

### <a name="metadata-structure"></a>元数据结构

内部照相机的设备元数据包的结构与任何其他设备的设备元数据包的结构相同。 设备元数据包内 **packageinfo.xml** 中的 MetadataKey 是使用 InternalDeviceModification 注册表项定义的模型 ID。 Windows 元数据系统基于模型 ID 下载设备元数据包。 不使用内部照相机的硬件 ID。

有关为 UWP 设备应用创建设备元数据的详细信息，请参阅 [构建 uwp 设备应用](the-workflow.md)。

### <a name="pre-installation"></a>安装前

使用 OEM 预安装工具包 (OPK) ，可以在设备上预安装 Microsoft Store 设备应用和设备元数据包。

## <a name="related-topics"></a>相关主题

[适用于内部设备的 UWP 设备应用](uwp-device-apps-for-specialized-devices.md)