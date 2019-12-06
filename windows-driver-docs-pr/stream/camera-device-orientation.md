---
title: 照相机方向驱动程序支持
description: 提供有关如何在设备上显式指定相机方向的信息。
ms.date: 08/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9390b49cc90c2e1370a164d5c486f1d9bdca58fe
ms.sourcegitcommit: 3ee05aabaf9c5e14af56ce5f1dde588c2c7eb4ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2019
ms.locfileid: "74881901"
---
# <a name="driver-support-for-camera-orientation"></a>照相机方向驱动程序支持

> [!IMPORTANT]
> 本主题后面所述的自动更正方法是相机传感器的非引用方向装载的*推荐*解决方案。 这是为了确保应用程序兼容性，因为已编写为使用相机源的大多数应用程序都不知道是否需要检查和更正旋转信息。 请仔细查看下面自动更正部分中的信息。

随着各种外形因素的计算设备的引入，某些物理约束导致相机传感器以非传统方向装入。 因此，有必要正确地描述 OS 和应用程序，如何装载传感器，以便能够正确呈现/记录所生成的视频。

从 Windows 10 版本1607开始，所有相机驱动程序都需要显式指定相机方向，而不考虑是否根据[最低硬件要求](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)装入相机。
具体而言，照相机驱动程序必须在与捕获设备接口关联的 ACPI \_PLD 结构中设置新引入的字段*旋转*：

```cpp
typedef struct _ACPI_PLD_V2_BUFFER {

    UINT32 Revision:7;
    UINT32 IgnoreColor:1;
    UINT32 Color:24;
    // …
    UINT32 Panel:3;         // Already supported by camera.
    // …
    UINT32 CardCageNumber:8;
    UINT32 Reference:1;
    UINT32 Rotation:4;      // 0 – Rotate by 0° clockwise
                            // 1 – Rotate by 45° clockwise (N/A to camera)
                            // 2 – Rotate by 90° clockwise
                            // 3 – Rotate by 135° clockwise (N/A to camera)
                            // 4 – Rotate by 180° clockwise
                            // 5 – Rotate by 225° clockwise (N/A to camera)
                            // 6 – Rotate by 270° clockwise
    UINT32 Order:5;
    UINT32 Reserved:4;

    //
    // _PLD v2 definition fields.
    //

    USHORT VerticalOffset;
    USHORT HorizontalOffset;
} ACPI_PLD_V2_BUFFER, *PACPI_PLD_V2_BUFFER;
```

对于照相机，ACPI \_PLD 结构中的 "**旋转**" 字段指定了度数（"0" 表示0度，"2" 表示 "90"，"4" 表示180度，"6" 表示270°）捕获帧相对于屏幕旋转，而显示处于其本机方向。

根据 "**旋转**" 字段中的值，应用程序可以执行其他旋转（如有必要），以便正确呈现捕获的帧。

## <a name="rotation-values"></a>旋转值

对于照相机和显示器共享同一架（或*机壳*/*大小写*）的那些设备，可以将这些外设装载到不同的表面上，每个外围设备在其各自平面上按固定的固定度数旋转。 因此，应用程序需要一种机制来描述两个外围设备之间的空间关系，以便能够以正确的方向将捕获的帧转到呈现图面上。

解决此问题的一种方法是使用 ACPI \_PLD 结构，此结构已定义了*表面*和*旋转度*的概念。 例如，"\_PLD" 结构已有指定外围设备所在表面的 *"panel"* 字段：

![ACPI PLD 面板字段](images/acpi-pld-panel-field.png)

### <a name="definition-of-acpi-_pld-panel-field-rev-50a"></a>ACPI \_PLD 面板字段的定义（Rev 5.0 a）

接下来的两个关系图直观地说明了每个面板的定义：

#### <a name="panel-definitions-for-desktop-pcs-and-most-devices"></a>台式计算机和大多数设备的面板定义

![面板定义-桌面](images/panel-definitions-desktop.png)

#### <a name="panel-definitions-for-foldable-devices"></a>适用于折叠设备的面板定义

![面板定义-折叠的设备](images/panel-definitions-foldable-devices.png)

事实上，Windows 已采用 ACPI "面板" 的概念，其中：

- 如果在固定位置静态装载了捕获设备，则照相机设备接口与 \_PLD 结构相关联，并相应地设置面板字段。

- 应用程序可以通过调用[DeviceInformation. EnclosureLocation](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.EnclosureLocation)属性，来检索捕获设备所在的面板。

ACPI \_PLD 结构还具有定义如下的旋转字段：

#### <a name="definition-of-acpi-_pld-rotation-field-rev-50a"></a>ACPI \_PLD 旋转字段的定义（Rev 5.0 a）

![ACPI \_PLD 旋转字段定义](./images/acpi-pld-rotation-field.png)

我们会进一步优化它以避免多义性，而不是按原样使用上面的定义：

- 对于照相机，ACPI \_PLD 结构中的 "旋转" 字段指定了度数（"0" 表示0度，"2" 表示 "90"，"4" 表示180度，"6" 表示270°）捕获帧相对于屏幕旋转，而显示处于其本机方向。

## <a name="landscape-primary-vs-portrait-primary"></a>横向主要与纵向主要副本

在 Windows 中，可以通过调用[DisplayInformation. NativeOrientation](https://docs.microsoft.com/uwp/api/Windows.Graphics.Display.DisplayInformation)（返回**横向**或**纵向**）来查询本机显示方向：

![显示本机方向扫描模式](./images/native-scanning-pattern.png)

无论**NativeOrientation**返回哪个值，逻辑显示扫描模式都从显示的左上角开始，从左到右移动（参见图5）。 对于默认物理方向为 "显式" 的那些设备，此属性不仅表示 ACPI*顶部*面板的位置，还提供照相机输出缓冲区与呈现图面之间的空间关系。

请注意，与相机不同的是， **NativeOrientation**属性不基于 ACPI，因此没有 \_PLD 结构。 即使将显示静态装载到设备也是如此。

## <a name="offset-mounting"></a>偏移量装入

强烈建议使用 IHV/Oem 以非0度偏移量来维护应用程序兼容性。 许多现有的和旧的应用程序不知道要查找 ACPI 的 PLD 表，也不会尝试更正非0度偏移量。 因此，对于此类应用，生成的视频将不会正确呈现。

如果在上述情况下，IHV/Oem 无法按0度方向装载传感器，则建议使用以下缓解步骤：

1. 自动更正照相机驱动程序中非0度方向（使用 AV 流微型端口驱动程序在内核模式下或在用户模式下使用设备 MFT 或 MFT0 等插件），使生成的输出帧处于0度方向。

1. 通过 FSSensorOrientation 标记声明非0度方向，使相机管道可以更正捕获的映像。

1. 如上所述，在 ACPI 的 PLD 表中声明非0度方向。

### <a name="compressedencoded-media-types"></a>压缩/编码的媒体类型

对于压缩的和/或编码的媒体类型（例如 MJPG、JPEG、H264、HEVC），无法使用正确的管道。 因此，如果 FSSensorOrientation 设置为非零值，压缩/编码的媒体类型将被筛选掉。

对于 MJPG 媒体类型（例如 UVC 相机中的媒体类型），框架服务器管道提供自动解码的媒体类型（NV12 或 YUY2 用于基于 DShow 的应用程序）。 将显示自动解码和更正后的媒体类型，但原始 MJPG 格式不会显示。

> [!备注！]如果必须向应用程序公开压缩/编码的媒体类型，则 IHV/Odm 不得使用 FSSensorOrientation 更正。 相反，必须由相机驱动程序（在内核模式下通过 AV 流驱动程序或在用户模式下通过 DMFT/MFT0）进行更正。

### <a name="auto-correct-via-av-stream-miniportdevice-mftmft0"></a>通过 AV 流微型端口/设备 MFT/MFT0 自动更正

如果传感器无法以0度的偏移量装入传感器，则*建议*使用以下方案：使 AV 流微型端口驱动程序（或以 DMFT 或 MFT0 形式提供的用户模式插入）更正生成的捕获帧，使其在0度偏移量上向管道公开。

从 AV 流微型端口和/或设备 MFT/MFT0 插件更正视频帧时，生成的媒体类型声明必须基于更正后的帧。 如果传感器按90度的偏移量装入，使生成的视频比传感器9:16 的高宽比，但更正后的视频为16:9，则媒体类型必须声明16:9 纵横比。

这包括生成的步幅信息。 这是必需的，因为由 IHV/OEM 控制负责执行更正的组件，并且相机管道不具有视频帧的可见性，但更正后除外。

强烈建议在用户模式下执行更正，并且必须遵循管道和用户模式插件之间的 API 协定。 具体而言，在使用 DMFT 或 MFT0 时，如果使用\_MFT 调用 IMFDeviceTransform：:P rocessMessage 或 IMFTransform：:P rocessMessage\_设置\_D3D\_MANAGER 消息，则用户模式插件必须遵循以下准则：

- 如果未提供 D3D 管理器（消息的 ulParam 为0），则用户模式插件不得调用任何 GPU 操作来处理旋转更正。 并且必须在系统内存中提供生成的帧。
- 如果提供了 D3D 管理器（消息的 ulParam 是 DXGI 管理器的 IUnknown），则必须使用 DXGI 管理器进行旋转更正，并且生成的帧必须为 GPU 内存。
- 用户模式插件还必须在运行时处理 D3D 管理器消息。 颁发 MFT\_消息\_设置\_D3D\_MANAGER 消息时，该插件生成的下一个帧必须与请求的内存类型（即，如果提供了 DXGI 管理器，则为 GPU，否则为 CPU）对应。
- 当 AV 流驱动程序（或用户模式插件）处理旋转更正时，ACPI 的 PLD 结构的旋转字段必须设置为0。

> [!NOTE]
> 使用 "自动更正" 时，Oem 和 Ihv 不得通过 \_PLD**旋转**字段来播发传感器的实际方向。 在这种情况下，**旋转**字段必须指示更正后的方向：0度。

## <a name="declare-via-fssensororientation"></a>通过 FSSensorOrientation 声明

```INF
; Defines the sensor mounting orientation offset angle in
; degrees clockwise.
FSSensorOrientation: REG_DWORD: 90, 180, 270
```

通过 FSSensorOrientation 注册表标记声明传感器的非0度方向，照相机管道可以在将捕获的帧呈现给应用程序之前对其进行更正。

管道将根据用例和应用请求/方案利用 GPU 或 CPU 资源来优化旋转逻辑。

### <a name="acpi-pld-rotation"></a>ACPI PLD 轮换

ACPI PLD 结构的旋转字段必须为0。 这是为了避免混淆可能使用 PLD 信息来更正帧的应用程序。

### <a name="media-type-information"></a>媒体类型信息

驱动程序提供的媒体类型必须是无法更正的媒体类型。 当使用 FSSensorOrientation 项通知非0度偏移量的相机管道时，该传感器提供的媒体类型信息必须是未更正的媒体类型。 例如，如果传感器装入了90度16:9 的顺时针偏移量，因此，生成的视频为9:16，则必须向照相机管道提供9:16 纵横比。

这是确保管道可正确配置计数器旋转进程所必需的：管道需要输入媒体类型和应用程序的所需输出媒体类型。

这包括步幅信息。 对于未更正的媒体类型，必须为相机管道提供 stride 信息。

### <a name="registry-subkey"></a>注册表子项

必须在 "设备接口" 节点上发布 "FSSensorOrientation" 注册表项。 推荐的方法是在照相机驱动程序的 INF 中，将此方法声明为 AddReg 指令。

FSSensorOrientation 中显示的数据必须为 REG\_DWORD，而接受的有效值为90、180和270。 其他任何值将被视为0度偏移量（即忽略）。

每个值都以顺时针度为单位表示传感器方向。 照相机管道将通过计数器以顺时针方向逆时针旋转视频来更正生成的视频帧：也就是说，90度顺时针声明会导致90度逆时针旋转，使生成的视频帧返回到0度偏移量。

### <a name="ms-os-descriptor-10"></a>MS OS 描述符1。0

对于基于 USB 的相机，还可以通过 MSO 描述符发布 FSSensorOrientation。

<!-- FIXME: Overview of OS descriptor could be removed -->
MS OS 描述符1.0 有两个组件：

- 固定长度标头部分
- 标头部分后面的一个或多个可变长度自定义属性部分

#### <a name="ms-os-descriptor-10-header-section"></a>MS OS 描述符1.0 标头部分

标头部分描述单个自定义属性（人脸身份验证配置文件）。

| 偏移量 | 字段      | 大小(字节) | Value  | 描述                     |
| ------ | ---------- | ------------ | ------ | ------------------------------- |
| 0      | dwLength   | 4            | \<\>   |                                 |
| 4      | bcdVersion | 2            | 0x0100 | 版本 1.0                     |
| 6      | wIndex     | 2            | 0x0005 | 扩展属性 OS 描述符 |
| 8      | wCount     | 2            | 0x0001 | 一个自定义属性             |

#### <a name="custom-ms-os-descriptor-10-property-section"></a>自定义 MS OS 描述符1.0 属性部分

| 偏移量 | 字段                | 大小(字节) | Value                              | 描述                                  |
| ------ | -------------------- | ------------ | ---------------------------------- | -------------------------------------------- |
| 0      | dwSize               | 4            | 0x00000036 （54）                    | 此属性的总大小（以字节为单位）。     |
| 4      | dwPropertyDataType   | 4            | 0x00000004                         | REG\_DWORD\_极少\_ENDIAN                   |
| 8      | wPropertyNameLength  | 2            | 0x00000024 （36）                    | 属性名称的大小（以字节为单位）。        |
| 10     | bPropertyName        | 50           | UVC-FSSensorOrientation            | Unicode 中的 "UVC-FSSensorOrientation" 字符串。 |
| 60     | dwPropertyDataLength | 4            | 0x00000004                         | 对于属性数据（sizeof （DWORD）），4个字节。   |
| 64     | bPropertyData        | 4            | 顺时针角度（以度为单位）。 | 有效值为90、180和270。           |

### <a name="ms-os-descriptor-20"></a>MS OS 描述符2。0

MSO 扩展描述符2.0 可用于定义注册表值以添加 FSSensorOrientation 支持。 这是使用[MICROSOFT OS 2.0 注册表属性描述符](uvc-camera-implementation-guide.md#microsoft-os-20-registry-property-descriptor)实现的。

对于 UVC FSSensorOrientation 注册表项，以下示例显示了一个示例 MSO 2.0 描述符集：

```cpp
UCHAR Example2_MSOS20DescriptorSet_UVCFSSensorOrientationForFutureWindows[0x3C] =
{
    //
    // Microsoft OS 2.0 Descriptor Set Header
    //
    0x0A, 0x00,                 // wLength - 10 bytes
    0x00, 0x00,                 // MSOS20_SET_HEADER_DESCRIPTOR
    0x00, 0x00, 0x0?, 0x06,     // dwWindowsVersion – 0x060?0000 for future Windows version
    0x4A, 0x00,                 // wTotalLength – 74 bytes

    //
    // Microsoft OS 2.0 Registry Value Feature Descriptor
    //
    0x40, 0x00,                 // wLength - 64 bytes
    0x04, 0x00,                 // wDescriptorType – 4 for Registry Property
    0x04, 0x00,                 // wPropertyDataType - 4 for REG_DWORD_LITTLE_ENDIAN
    0x32, 0x00,                 // wPropertyNameLength – 50 bytes
    0x55, 0x00, 0x56, 0x00,     // Property Name - "UVC-FSSensorOrientation"
    0x43, 0x00, 0x2D, 0x00,
    0x46, 0x00, 0x53, 0x00,
    0x53, 0x00, 0x65, 0x00,
    0x6E, 0x00, 0x73, 0x00,
    0x6F, 0x00, 0x72, 0x00,
    0x4F, 0x00, 0x72, 0x00,
    0x69, 0x00, 0x65, 0x00,
    0x6E, 0x00, 0x74, 0x00,
    0x61, 0x00, 0x74, 0x00,
    0x69, 0x00, 0x6F, 0x00,
    0x6E, 0x00, 0x00, 0x00,
    0x00, 0x00,
    0x04, 0x00,                 // wPropertyDataLength – 4 bytes
    0x5A, 0x00, 0x00, 0x00      // PropertyData – 0x0000005A (90 degrees offset)
}
```

## <a name="declare-via-acpi-pld-information"></a>通过 ACPI PLD 信息声明

作为最后手段的一项选择，可以按上述方式利用 PLD 信息，以向应用程序指示必须先更正视频帧，然后才能呈现/编码。 但正如前文所述，许多现有应用程序不使用 PLD 信息，也不处理帧旋转，因此，在某些情况下，应用程序可能无法正确呈现结果视频。

下图说明了每个硬件配置 \_PLD 旋转字段的值：

### <a name="rotation-0-degree-clockwise"></a>旋转：0度顺时针

![0度旋转图](./images/rotation-0-degree-reference-orientation.png)

如上图所示：

- 左侧的图片说明了要捕获的场景。

- 下图描绘了一个 CMOS 传感器的场景的查看方式，该感应器的物理读出顺序从左下角开始从左到右移动。

- 右边的图片表示照相机驱动程序的输出。 在此示例中，可以在显示为其本机方向时直接呈现媒体缓冲区的内容，而无需额外旋转。 因此，ACPI \_PLD 旋转字段的值为0。

### <a name="rotation-90-degrees-clockwise"></a>旋转：顺时针90度

![90度旋转图](./images/rotation-90-degrees-clockwise.png)

在这种情况下，与原始场景相比，媒体缓冲区的内容会顺时针旋转90度。 因此，ACPI \_PLD 旋转字段的值为2。

### <a name="rotation-180-degrees-clockwise"></a>旋转：顺时针180度

![180度旋转图](./images/rotation-180-degrees-clockwise.png)

在这种情况下，与原始场景相比，媒体缓冲区的内容会顺时针旋转180度。 因此，ACPI \_PLD 旋转字段的值为4。

### <a name="rotation-270-degrees-clockwise"></a>旋转：顺时针270度

![270度旋转图](./images/rotation-270-degrees-clockwise.png)

在这种情况下，与原始场景相比，媒体缓冲区的内容会顺时针旋转270度。 因此，ACPI \_PLD 旋转字段的值为6。
