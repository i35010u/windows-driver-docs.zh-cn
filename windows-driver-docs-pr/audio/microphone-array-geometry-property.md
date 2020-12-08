---
title: 麦克风阵列几何属性
description: 麦克风阵列几何属性
keywords:
- 麦克风阵列 WDK 音频
- 几何描述符 WDK 音频
- 麦克风阵列 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5c98629bf838eb61d159a46eda94835271d11d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801025"
---
# <a name="microphone-array-geometry-property"></a>麦克风阵列几何属性


在 Windows Vista 和更高版本中，为麦克风阵列提供了支持。 在大多数情况下，在便携式计算机或监视器中嵌入的单个麦克风无法很好地捕获声音。 麦克风数组更好地用于隔离声源，并拒绝环境噪音和 reverberation。 [**KSPROPERTY \_ 音频 \_ MIC \_ array \_ GEOMETRY**](./ksproperty-audio-mic-array-geometry.md)属性指定麦克风阵列的几何。 属性值 [**KSAUDIO \_ MIC \_ ARRAY \_ GEOMETRY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mic_array_geometry)描述数组类型 (线性、平面等) 、数组中的麦克风数量和其他功能。

本主题介绍外部 USB 麦克风阵列如何使用随 Windows Vista 提供的麦克风阵列支持。 外部 USB 麦克风阵列必须提供描述其数组的几何和其他功能所需的参数，以响应 **获取 \_ 内存** 请求。

USB 麦克风阵列使用标准格式来提供几何信息。 Windows Vista USB 音频类驱动程序在读取几何信息时必须使用相同的格式。 有关标准格式的详细信息，请参阅 [麦克风数组几何描述符格式](microphone-array-geometry-descriptor-format.md)。

应用程序可以调用 [IPart：： GetSubType](/windows/win32/api/devicetopology/nf-devicetopology-ipart-getsubtype) 来检索有关插孔的信息，以确定插入插孔的设备是否为麦克风阵列。 **IPart：： GetSubType** 返回表示输入插孔类型的 PIN 类别 GUID。 如果插入的设备是麦克风阵列，则返回的 GUID 等于 KSNODETYPE \_ 麦克风 \_ 阵列。 该应用程序还可以帮助你确定是否已将麦克风阵列插入错误的插孔。 在后一种情况下，返回的 pin 类别 GUID 可用于其他设备，也可能表示没有设备插入麦克风插孔。 有关 pin 类别 Guid 的详细信息，请参阅 [固定类别属性](pin-category-property.md)。

在应用程序发现插入正确输入插孔的麦克风阵列后，下一步是确定该阵列的几何。 有三种基本的几何图形： *线性*、 *平面* 和三维 *(3-d)*。 几何信息还提供了每个麦克风的频率范围和 x y z 坐标等详细信息。

下面的代码示例演示了 \_ \_ \_ 音频驱动程序用于描述外部 USB 麦克风阵列的 KSAUDIO MIC 数组几何结构：

```cpp
KSAUDIO_MIC_ARRAY_GEOMETRY mic_Array =
{
 0x100,// usVersion (1.0)
 KSMICARRAY_MICARRAYTYPE_LINEAR,// usMicArrayType
 7854,  // wVerticalAngleBegin (45 deg; PI/4 radians x 10000)
 -7854,  // wVerticalAngleEnd
 0, // lHorizontalAngleBegin
 0, // lHorizontalAngleEnd
 25, // usFrequencyBandLo in Hz
 19500, // usFrequencyBandHi in Hz
 2,  // usNumberOfMicrophones
 ar_mic_Coordinates // KsMicCoord
};
```

在上面的代码示例中，ar \_ mic \_ 坐标变量是 KSAUDIO \_ 麦克风坐标结构的数组 \_ ，它包含麦克风阵列中麦克风的坐标。

下面的代码示例演示如何使用 ar \_ mic \_ 坐标数组描述麦克风阵列中麦克风的几何位置，如前面的代码示例中所述：

```cpp
KsMicCoord ar_mic_Coordinates[] =
{
 // Array microphone 1
 {
  KSMICARRAY_MICTYPE_CARDIOID,// usType
  100, // wXCoord (mic elements are 200 mm apart)
  0,// wYCoord 
  0, // wZCoord 
  0,// wVerticalAngle
  0,// wHorizontalAngle
 },
 // Array microphone 2
 {
  KSMICARRAY_MICTYPE_CARDIOID,// usType
  -100, // wXCoord 
  0,// wYCoord 
  0, // wZCoord 
  0,// wVerticalAngle
  0,// wHorizontalAngle
 }
};
```

在上面的代码示例中，为麦克风阵列中的每个麦克风指定了 x y z 坐标，同时还为了描述其有效工作区的垂直和水平角。

若要修改 Micarray MSVAD 示例驱动程序以提供虚拟麦克风阵列的阵列几何信息，必须执行以下任务。

首先，导航到 Src \\ 音频 \\ Msvad \\ Micarray 并找到 Mintopo 文件。 编辑 Mintopo 中的属性处理程序部分，以便 KSAUDIO \_ MIC \_ array \_ GEOMETRY 结构包含有关麦克风数组的信息。 下面的代码示例演示了必须修改的代码的特定部分：

```cpp
// Modify this portion of PropertyHandlerMicArrayGeometry
PKSAUDIO_MIC_ARRAY_GEOMETRY pMAG = (PKSAUDIO_MIC_ARRAY_GEOMETRY)PropertyRequest->Value;

// fill in mic array geometry fields
pMAG->usVersion = 0x0100;           // Version of Mic array specification (0x0100)
pMAG->usMicArrayType = (USHORT)KSMICARRAY_MICARRAYTYPE_LINEAR;        // Type of Mic Array
pMAG->wVerticalAngleBegin = -7854;  // Work Volume Vertical Angle Begin (-45 degrees)
pMAG->wVerticalAngleEnd   =  7854;  // Work Volume Vertical Angle End   (+45 degrees)
pMAG->wHorizontalAngleBegin = 0;    // Work Volume Horizontal Angle Begin
pMAG->wHorizontalAngleEnd   = 0;    // Work Volume Horizontal Angle End
pMAG->usFrequencyBandLo = 100;      // Low end of Freq Range
pMAG->usFrequencyBandHi = 8000;     // High end of Freq Range
 
pMAG->usNumberOfMicrophones = 2;    // Count of microphone coordinate structures to follow.

pMAG->KsMicCoord[0].usType = (USHORT)KSMICARRAY_MICTYPE_CARDIOID;          
pMAG->KsMicCoord[0].wXCoord = -100; // mic elements are 200 mm apart
pMAG->KsMicCoord[0].wYCoord = 0;         
pMAG->KsMicCoord[0].wZCoord = 0;         
pMAG->KsMicCoord[0].wVerticalAngle = 0;  
pMAG->KsMicCoord[0].wHorizontalAngle = 0;

pMAG->KsMicCoord[1].usType = (USHORT)KSMICARRAY_MICTYPE_CARDIOID;          
pMAG->KsMicCoord[1].wXCoord = 100;  // mic elements are 200 mm apart
pMAG->KsMicCoord[1].wYCoord = 0;         
pMAG->KsMicCoord[1].wZCoord = 0;         
pMAG->KsMicCoord[1].wVerticalAngle = 0;  
pMAG->KsMicCoord[1].wHorizontalAngle = 0;
```

前面的代码示例显示了为具有两个麦克风元素的线性麦克风数组提供的信息，其中每个元素都是一个 cardioid 类型，并从该数组的中心找到 100 mm。

对于第二个修改，请编辑 Msvad 文件，如 [Msvad Micarray 的修改 inf](modified-inf-for-msvad-micarray.md)中所示。

完成文件修改后，请完成以下过程，为麦克风阵列构建并安装示例驱动程序。

1.  启动要在其中工作的 WDK 生成环境。 例如，x86 免费生成环境。

2.  导航到 Src \\ 音频 \\ Msvad 文件夹。

3.  键入 " **生成** " 命令，然后按 "enter"。

4.  将修改后的 Msvad 文件复制到生成过程创建的以下文件夹中：

    Src \\ 音频 \\ Msvad \\ Micarray \\ objfre \_ wlh \_ x86 \\ i386

5.  验证步骤4中的文件夹是否包含名为 Vadarray.sys 的文件。

6.  打开 "控制面板"，并使用 " **添加硬件** " 手动安装示例驱动程序。

7.  在 "控制面板" 中打开 " **声音** 小程序"，然后单击 " **录制** " 选项卡，验证是否可以看到刚刚安装的虚拟麦克风阵列。

有关如何开发应用程序来发现麦克风阵列的信息，请参阅 [如何构建和使用适用于 Windows Vista 的麦克风阵列](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/MicArrays_guide.doc)的附录 C。

 

