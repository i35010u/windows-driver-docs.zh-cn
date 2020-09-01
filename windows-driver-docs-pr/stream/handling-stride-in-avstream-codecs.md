---
title: 处理 AVStream 编解码器中的步幅
description: 处理 AVStream 编解码器中的步幅
ms.assetid: 816a0ddc-8ab8-4259-9842-76f5e4dadee0
keywords:
- AVStream 硬件编解码器支持 WDK，处理步幅
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a69f553984b4ee3390f52406e13869f3a3d62a4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190571"
---
# <a name="handling-stride-in-avstream-codecs"></a>处理 AVStream 编解码器中的步幅


当解码器连接到呈现器（如增强的视频呈现器） (EVR) 或支持 Direct3D 的组件时，微型驱动程序会收到 D3D 缓冲区而不是系统内存缓冲区。

不同于系统内存缓冲区，在呈现之前必须将其复制到 D3D 面，而 D3D 缓冲区可以直接由呈现引擎显示。 因此，通过使用 D3D 缓冲区而不是系统内存缓冲区，微型驱动程序为每个缓冲区保存复制操作。

当支持舍弃的微型驱动程序收到 D3D 缓冲区时，D3D 图面将被锁定，指向它的指针位于 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)中。**数据**。 在 KSSTREAM 标头的 [**KS \_ 帧 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info) 扩展中提供 surface stride 信息 \_ ，如下面的代码示例所示：

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

微型驱动程序应使用[**KS \_ BITMAPINFOHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)结构的**biWidth**成员作为表面宽度。

 ([**KS \_ VIDEOINFOHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)。**bmiHeader** 的类型为 KS \_ BITMAPINFOHEADER。 [**KS \_DATARANGE \_ 视频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)。**VideoInfoHeader** 的类型为 KS \_ VideoInfoHeader。 ) 

如果是 KS \_ 帧 \_ 信息。**lSurfacePitch** 有一个非零值，则微型驱动程序必须使用 **lSurfacePitch** 作为相关 KSSTREAM 标头中指定的缓冲区的宽度/步幅 \_ 。 否则，输出图像会出现乱码。

 

