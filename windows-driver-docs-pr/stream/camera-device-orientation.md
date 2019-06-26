---
title: 对照相机方向的驱动程序支持
description: 提供有关如何显式指定的设备上的照相机方向信息。
ms.date: 08/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 63a4a75c684aa7bba39853636ce171edc432ac63
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386691"
---
# <a name="driver-support-for-camera-orientation"></a>对照相机方向的驱动程序支持



> [!IMPORTANT]
> 本主题后面所述的自动更正的方法是*建议*非引用方向装载的相机传感器的解决方案。 这是为了确保应用程序兼容性，因为大部分应用程序已编写为使用的相机源不知道检查，也不能更正旋转信息。 请仔细查看下面的自动更正部分中的信息。

Window 10，版本 1607 中，从相机的所有驱动程序所需显式指定照相机方向而不考虑如果照相机装载根据[最低硬件要求](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)。

具体而言，照相机驱动程序必须将一个新**旋转**字段中的 ACPI\_以前结构与捕获设备接口相关联：

```cpp
typedef struct _ACPI_PLD_V2_BUFFER {

    UINT32 Revision:7;
    UINT32 IgnoreColor:1;
    UINT32 Color:24;
    // ...
    UINT32 Panel:3; // Already supported by camera.
    // ...
    UINT32 CardCageNumber:8;
    UINT32 Reference:1;
    UINT32 Rotation:4;  // 0 – Rotate by 0° clockwise
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

 } ACPI_PLD_V2_BUFFER, *PACPI_PLD_V_BUFFER;
 ```

用于相机，**旋转**字段中的 ACPI\_以前结构指定的数量度为单位 （0，为 0 °，90 °，'4' 180 °，为"2"和"6 270 度) 捕获的帧进行旋转相对于屏幕中显示时其本机方向。

根据中的值**旋转**字段中，如有必要，以便正确呈现捕获的帧，应用程序可以执行其他旋转。

## <a name="design-overview"></a>设计概述


对于这些设备的照相机和显示共享同一个底座或*机箱*/*大小写*（手机、 平板电脑、 笔记本电脑和-一体 Pc） 很可能能够将这些外围设备安装在不同的图面 （前端/后端、 顶部/底部或对机箱的左/右图面） 与每个正在 （通常限制为 0、 90、 180 或 270 度顺时针旋转在实践中） 及其各自平面上固定但任意度的旋转角度。 请注意，传统桌面 Pc 不属于相机作为此类别和通常作为外部外围设备连接的显示，它们可以以物理方式操作在 3D 空间中在运行时。

因此，应用程序需要一种机制，以说明两个外围设备之间的空间关系，以便捕获的帧可以转置到正确的方向呈现图面上。

若要解决此问题的一种方法是使用 ACPI\_以前结构，其中已有的概念*图面*并*旋转的度数*定义。 请参阅[ACPI 规范](https://uefi.org/specifications)并[ACPI 支持文档](https://uefi.org/acpi)的完整规范。 例如，\_以前结构已*面板*字段指定外围设备所在的图面：

![ACPI 以前面板字段](images/acpi-pld-panel-field.png)

*ACPI 定义\_以前面板字段 (修订版 5.0 a)*

接下来两个关系图直观地说明了每个面板的定义：

![面板定义-桌面](images/panel-definitions-desktop.png)

*桌面 Pc 和大多数设备的面板定义*

![面板中定义的可折叠的设备](images/panel-definitions-foldable-devices.png)

*设备可折叠的面板定义*

这一概念的 ACPI*面板*Windows 已采用其中：

-   照相机设备接口是与相关联\_以前结构与面板字段正在相应地设置，如果捕获设备以静态方式装载在固定位置。

-   应用程序可以检索捕获设备通过调用其驻留的面板[Windows.Devices.Enumeration.DeviceInformation.EnclosureLocation.Panel](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration.EnclosureLocation#Windows_Devices_Enumeration_EnclosureLocation_Panel)属性。

ACPI\_以前结构还有**旋转**字段定义如下：

![ACPI 以前旋转字段](images/acpi-pld-rotation-field.png)

*ACPI 定义\_以前旋转字段 (Rev 5.0 a)*

而不是使用上述"按原样"的定义，我们将进一步优化，以便避免多义性：

- 用于相机，**旋转**字段中的 ACPI\_以前结构指定的数量度为单位 （0，为 0 °，90 °，'4' 180 °，为"2"和"6 270 度) 捕获的帧进行旋转相对于屏幕中显示时其本机方向。

## <a name="landscape-primary-vs-portrait-primary"></a>前景主 vs。纵向主

具体取决于外形规格中，设备可能定义为主要横向或纵向主，这指从返回的值[Windows.Graphics.Display.DisplayInformation.NativeOrientation](https://docs.microsoft.com/uwp/api/Windows.Graphics.Display.DisplayInformation#Windows_Graphics_Display_DisplayInformation_NativeOrientation)属性。

无论设备是横向还是纵向主的 ACPI 定义*原点*始终是面板左下的角，因为用户面向面板。 相机传感器的建议的装载方向是传感器的这样的扫描行是传感器的从左到右的 ACPI 面板左下角 (origin) 从水平到右下角。

这是传感器引用方向。

![前景主-传感器扫描方向](images/landscape-primary-sensor-scan-direction.png)

*横向 Primary:传感器扫描方向*

同样，为纵向主引用方向传感器的是因为 diagramed 如下：

![纵向主-传感器扫描方向](images/portrait-primary-sensor-scan-direction.png)

*纵向 Primary:传感器扫描方向*

这可确保当回转仪/加速度传感器生成通知的设备的相对方向，回转仪/加速感应器的参考点是符合传感器的参考方向：即，应用只需获取设备的相对方向并调整媒体框架仅基于该信息。

## <a name="non-reference-orientation-mounting"></a>非引用方向装载


由于硬件/窗体身份限制，通常传感器需要从引用方向装入某偏移量处。 完成此操作后，OEM/IHV 必须实现以下两个解决方案之一：

1.  **建议**:自动更正方向。 传感器驱动程序和照相机驱动程序必须创建两个的驱动程序，以指示当前的传感器方向并具有"正确"生成帧照相机的驱动程序堆栈之间的自定义协议。

2.  指示中的偏移量\_以前**旋转**字段。

### <a name="auto-correct"></a>自动更正

这是*建议*引用方向装载的相机传感器的解决方案。 这是为了确保应用程序兼容性，因为大部分应用程序已编写为使用的相机源不知道检查，也不能更正旋转信息。

这包括任何 DirectShow 的应用程序和大多数基于 MF/MediaCapture 应用程序。

> [!NOTE]
> 使用自动正确时，Oem 和 Ihv 必须不播发通过传感器的实际方向\_以前**旋转**字段。 在这种情况下，**旋转**字段必须指示更正后的方向：0 度。

### <a name="pld-rotation"></a>\_以前旋转

如果硬件约束限制范围内自动更正捕获的帧中，从系统建议的解决方案，以指示从引用方向的偏移量，因此旋转识别应用程序可以补偿。

此解决方案不理想，因为如上面所述，许多现有应用程序执行不处理 （或甚至预期） 引用方向**旋转**信息。 这将导致应用程序捕获和呈现不正确的方向的视频帧的结束位置的重要应用程序兼容性问题。

下图显示了的值\_以前**旋转**字段中为每个硬件配置：

**旋转：0 度顺时针 （引用方向）**

![旋转 0 度顺时针旋转的引用页面方向](images/rotation-0-degree-reference-orientation.png)

在上面的关系图：

-   在左侧的图片说明了场景中，从而捕获。

-   在中间图描述了其物理读数顺序从左到右向上移动左下角开始 CMOS 传感器场景的查看方式。 在硬件级别 CMOS 传感器在此示例中在垂直方向，但不能水平翻转场景。

-   在右侧的图片表示照相机的驱动程序的输出。 在此示例中，媒体缓冲区的内容可以呈现直接显示时其本机方向而无需其他旋转。 因此，ACPI\_以前**旋转**字段的值为 0。



**旋转：顺时针旋转 90 度**

![旋转的顺时针旋转 90 度](images/rotation-90-degrees-clockwise.png)

在这种情况下，媒体缓冲区的内容被旋转 90 度顺时针旋转相比原始场景。 因此，ACPI\_以前**旋转**字段的值为 2。

应用程序读取\_以前**旋转**信息会通过逆时针旋转 90 度的生成的图像校正图像顺时针旋转计数器。



**旋转的顺时针旋转 180 度**

![旋转的顺时针旋转 180 度](images/rotation-180-degrees-clockwise.png)

在这种情况下，媒体缓冲区的内容旋转 180 度顺时针旋转相比原始场景。 因此，ACPI\_以前**旋转**字段的值为 4。

应用程序读取\_以前**旋转**信息会更正通过逆时针旋转 180 度的生成的图像的图像。



**旋转：顺时针旋转 270 度**

![旋转的顺时针旋转 270 度](images/rotation-270-degrees-clockwise.png)

在这种情况下，媒体缓冲区的内容旋转 270 度顺时针旋转相比原始场景。 因此，ACPI\_以前**旋转**字段的值为 6。

应用程序读取\_以前**旋转**信息会更正通过逆时针旋转 90 度顺时针旋转生成的图像的图像 （等效于 270 度顺时针旋转计数器）。


