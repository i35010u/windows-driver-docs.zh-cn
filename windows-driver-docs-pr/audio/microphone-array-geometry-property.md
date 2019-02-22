---
title: 麦克风阵列 Geometry 属性
description: 麦克风阵列 Geometry 属性
ms.assetid: 7f280677-f86d-4687-b992-e2580046bd57
keywords:
- mic 数组 WDK 音频
- geometry 描述符 WDK 音频
- 麦克风阵列 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51a9ca3ddc96b3ece4005691749373dfc0f9d2d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534303"
---
# <a name="microphone-array-geometry-property"></a>麦克风阵列 Geometry 属性


在 Windows Vista 及更高版本，提供的麦克风阵列支持。 在大多数情况下，单个麦克风嵌入在便携式计算机或监视器不会捕获声音很好。 麦克风的数组执行更好地找出声音源并拒绝避免环境噪音和混响。 [ **KSPROPERTY\_音频\_MIC\_数组\_GEOMETRY** ](https://msdn.microsoft.com/library/windows/hardware/ff537289)属性指定几何图形的麦克风阵列。 属性值， [ **KSAUDIO\_MIC\_数组\_GEOMETRY**](https://msdn.microsoft.com/library/windows/hardware/ff537087)，描述的数组类型 （线性、 平面，等等），数组中的麦克风的数量和其他功能。

本主题介绍如何外部 USB 麦克风阵列可以使用麦克风阵列支持随附于 Windows Vista。 外部 USB 麦克风数组必须提供用于描述几何和其他功能以响应其数组所需的参数**获取\_内存优化**请求。

USB 麦克风阵列使用标准格式提供几何信息。 读取的几何信息时，Windows Vista USB 音频类驱动程序必须使用相同的格式。 有关标准格式的详细信息，请参阅[麦克风阵列 Geometry 描述符格式](microphone-array-geometry-descriptor-format.md)。

应用程序可以调用[IPart::GetSubType](https://go.microsoft.com/fwlink/p/?linkid=143726)来检索有关一个插孔，若要确定是否已插入插孔设备麦克风阵列的信息。 **IPart::GetSubType**返回 pin 类别 GUID，表示输入的插孔类型。 如果已接通电源的设备为麦克风数组，返回的 GUID 是否等于 KSNODETYPE\_麦克风\_数组。 应用程序还有助于您确定是否插入您的麦克风阵列插入错误插孔。 在后一种方案中，返回的 pin 类别 GUID 是为不同的设备或它指示没有插入麦克风的插孔的设备。 有关 pin 类别 Guid 的详细信息，请参阅[Pin Category 属性](pin-category-property.md)。

应用程序发现已插入正确的输入插孔麦克风阵列后下, 一步是确定数组的几何图形。 有三个基本几何：*线性*，*平面*，并*三个三维 (3-D)*。 几何信息还提供了详细信息，例如频率范围和每个麦克风的 x y z 坐标。

下面的代码示例显示了 KSAUDIO\_MIC\_数组\_音频驱动程序使用来描述一个外部 USB 麦克风阵列的几何结构：

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

在前面的代码示例，ar\_mic\_坐标变量为数组 KSAUDIO\_麦克风\_坐标结构，它包含麦克风麦克风数组中的坐标。

下面的代码示例演示如何 ar\_mic\_坐标数组用于描述几何麦克风麦克风数组中的位置，如前面的代码示例中所述：

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

在前面的代码示例中，针对每个麦克风中麦克风阵列，以及描述其有效的工作区的垂直和水平角度提供 x y z 坐标。

若要修改 Micarray MSVAD 示例驱动程序提供虚拟麦克风阵列的阵列几何信息，必须执行以下任务。

首先，导航到 Src\\音频\\Msvad\\Micarray 并找到 Mintopo.cpp 文件。 编辑 Mintopo.cpp 中的属性处理程序部分，以便 KSAUDIO\_MIC\_数组\_几何结构包含关于麦克风阵列的信息。 必须修改的代码的特定部分下面的代码示例所示：

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

前面的代码示例显示了具有两个麦克风元素，其中每个是 cardioid 类型，位于从数组的中心 100 mm 为线性的麦克风阵列提供信息。

对于第二处修改，编辑 Msvad.inf 文件中所示[MSVAD Micarray 用于修改 INF](modified-inf-for-msvad-micarray.md)。

完成文件的修改后，完成以下过程来生成和安装麦克风阵列的示例驱动程序。

1.  启动 WDK 构建环境，你想要在其中。 例如，x86 Free Build Environment。

2.  导航到 Src\\音频\\Msvad 文件夹。

3.  类型**生成**命令，，然后按 Enter。

4.  将修改后的 Msvad.inf 文件复制到生成过程创建的以下文件夹：

    Src\\Audio\\Msvad\\Micarray\\objfre\_wlh\_x86\\i386

5.  验证在步骤 4 中的文件夹包含一个名为 Vadarray.sys 文件。

6.  打开控制面板，然后使用**添加硬件**手动安装的示例驱动程序。

7.  打开**声音**小程序在控制面板中单击**录制**选项卡上验证是否可以看到虚拟数组您刚安装的麦克风。

有关如何开发应用程序能够发现麦克风阵列的信息，请参阅的附录 C[如何与生成和使用麦克风阵列适用于 Windows Vista 的](https://go.microsoft.com/fwlink/p/?linkid=306613)。

 

 




