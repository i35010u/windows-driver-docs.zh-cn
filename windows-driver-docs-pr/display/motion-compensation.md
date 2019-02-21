---
title: 运动补偿
description: 运动补偿
ms.assetid: 3b5c91f9-6c22-4110-943a-5b833f32c014
keywords:
- 绘制 WDK DirectDraw，运动补偿
- DirectDraw WDK Windows 2000 显示，运动补偿
- 运动补偿 WDK
- 压缩的视频解码 WDK DirectDraw
- 视频解码 WDK DirectDraw
- 解码 WDK DirectDraw
- 数字视频解码 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 746476b34371e33ce1e161ed338560b44eac3e48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519731"
---
# <a name="motion-compensation"></a>运动补偿


## <span id="ddk_motion_compensation_gg"></span><span id="DDK_MOTION_COMPENSATION_GG"></span>


运动补偿是压缩数字视频解码过程的重要阶段使用的术语。 许多图形加速器设备提供某种类型的加速功能支持压缩的视频解码。 由于运动补偿过程是最常支持的视频解码部分，支持压缩的视频解码的设备驱动程序接口称为 DDI 的运动补偿。 除了运动补偿，某些设备可以执行 IDCT （反离散余弦值转换） 和软件视频解码器可用于加速解码过程其他硬件功能。 运动补偿 DDI 的灵活程度足以到句柄提供这些以及其他功能的设备。

对输入的数据和软件 MPEG 解码器是定义完善的。 如果解码器专为 mpeg-2，输入是以 mpeg-2 格式。 也定义解码器的输出。 它是未压缩的框架中以不同的格式。 但是，此期间软件解码器之间设置格式和显示设备不是定义完善的许多设备都需要其自己的专有数据格式。 因此，运动补偿设备驱动程序接口是灵活并且临时格式被描述为 Guid。 显示驱动程序报告表示它支持的功能的 Guid 和软件解码器选择最符合其要求的 GUID。

若要启用运动补偿功能，该驱动程序必须执行以下步骤：

-   实现[ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)函数，并设置**GetDriverInfo**隶属[ **DD\_HALINFO**](https://msdn.microsoft.com/library/windows/hardware/ff551627)结构，以指向此函数时[ **DrvGetDirectDrawInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff556229)调用。 在驱动程序*DdGetDriverInfo*函数必须分析 GUID\_MotionCompCallbacks GUID。

-   填写[ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)用相应的驱动程序回调指针和回调类型标志时设置的结构*DdGetDriverInfo*函数调用使用 GUID\_MotionCompCallbacks GUID。 该驱动程序必须随后将此初始化的结构复制到 Microsoft DirectDraw 分配缓冲区所属**lpvData**的成员[ **DD\_GETDRIVERINFODATA**](https://msdn.microsoft.com/library/windows/hardware/ff551550)结构点，并返回到缓冲区中写入的字节数**dwActualSize**。

 

 





