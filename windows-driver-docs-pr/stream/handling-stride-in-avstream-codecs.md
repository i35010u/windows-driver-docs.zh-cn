---
title: 处理 AVStream 编解码器中的步幅
description: 处理 AVStream 编解码器中的步幅
ms.assetid: 816a0ddc-8ab8-4259-9842-76f5e4dadee0
keywords:
- AVStream 硬件编解码器支持 WDK，处理步幅
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b483577a30e0d6cacb9e73af6fb6e74f508d194f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838778"
---
# <a name="handling-stride-in-avstream-codecs"></a>处理 AVStream 编解码器中的步幅


当解码器连接到呈现器（如增强视频呈现器（EVR））或支持 Direct3D 的组件时，微型驱动程序会收到 D3D 缓冲区而不是系统内存缓冲区。

不同于系统内存缓冲区，在呈现之前必须将其复制到 D3D 面，而 D3D 缓冲区可以直接由呈现引擎显示。 因此，通过使用 D3D 缓冲区而不是系统内存缓冲区，微型驱动程序为每个缓冲区保存复制操作。

当支持舍弃的微型驱动程序接收 D3D 缓冲区时，D3D 图面将被锁定，指向它的指针位于[**KSSTREAM\_标题**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)中。**数据**。 如以下代码示例中所示，在[**KS\_帧\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_frame_info) EXTENSION to KSSTREAM\_标头中提供 surface 步幅信息：

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

微型驱动程序应使用[**KS\_BITMAPINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)结构的**biWidth**成员作为表面宽度。

（[**KS\_VIDEOINFOHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_videoinfoheader)。**bmiHeader**的类型为 KS\_BITMAPINFOHEADER。 [**KS\_DATARANGE\_视频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_datarange_video)。**VideoInfoHeader**的类型为 KS\_VideoInfoHeader。）

如果 KS\_帧\_信息。**lSurfacePitch**有一个非零值，则微型驱动程序必须使用**lSurfacePitch**作为在相关 KSSTREAM\_标题中指定的缓冲区的宽度/步幅。 否则，输出图像会出现乱码。

 

 




