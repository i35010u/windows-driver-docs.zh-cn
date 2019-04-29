---
title: 处理 AVStream 编解码器中的步幅
description: 处理 AVStream 编解码器中的步幅
ms.assetid: 816a0ddc-8ab8-4259-9842-76f5e4dadee0
keywords:
- AVStream 硬件编解码器支持 WDK，处理 stride
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5de3736283b0696c18a771971bb8e33241a5d74
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363507"
---
# <a name="handling-stride-in-avstream-codecs"></a>处理 AVStream 编解码器中的步幅


当解码器连接到如增强的视频呈现器 (EVR) 或一个组件，支持 Direct3D 呈现器时，微型驱动程序将接收 D3D 缓冲区而不是系统内存缓冲区。

与不同的系统内存缓冲区，必须将复制到 D3D 面呈现之前，可以直接通过呈现引擎显示 D3D 缓冲区。 因此，通过使用 D3D 缓冲区而不系统内存缓冲区，微型驱动程序将保存每个缓冲区复制操作。

如果支持工棚的微型驱动程序收到 D3D 缓冲区、 D3D 图面已锁定，并且位于一个指针指向它[ **KSSTREAM\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567138)。**数据**。 中提供的图面上 stride 信息[ **KS\_帧\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff567645)扩展 KSSTREAM\_标头，如下面的代码示例中所示：

```cpp
typedef struct KS_FRAME_INFO {
    ULONG                   ExtendedHeaderSize; // Size of this extended header
    DWORD                   dwFrameFlags;       // Field1, Field2, or Frame
    LONGLONG                PictureNumber;
    LONGLONG                DropCount;

    // The following are only set when you use OverlayMixer
    HANDLE                  hDirectDraw;        // user mode DDraw handle
    HANDLE                  hSurfaceHandle;     // user mode surface handle
    RECT                    DirectDrawRect;     // portion of surface locked
    union {
  LONG               lSurfacePitch;  // Contains surface pitch a.k.a stride
         DWORD              Reserved1;
    };
    // Reserved fields, never reference these
    DWORD                   Reserved2;
    DWORD                   Reserved3;
    DWORD                   Reserved4;
} KS_FRAME_INFO, *PKS_FRAME_INFO;
```

微型驱动程序应使用**biWidth**的成员[ **KS\_BITMAPINFOHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff567305)结构作为图面上的宽度。

([**KS\_VIDEOINFOHEADER**](https://msdn.microsoft.com/library/windows/hardware/ff567700)。**bmiHeader**属于类型 KS\_BITMAPINFOHEADER。 [**KS\_DATARANGE\_视频**](https://msdn.microsoft.com/library/windows/hardware/ff567628)。**VideoInfoHeader**属于类型 KS\_VIDEOINFOHEADER。)

如果 KS\_帧\_信息。**lSurfacePitch**具有非零值，微型驱动程序必须使用**lSurfacePitch**作为相关 KSSTREAM 中指定的缓冲区的宽度/步幅\_标头。 否则，输出图像将显示出现乱码。

 

 




