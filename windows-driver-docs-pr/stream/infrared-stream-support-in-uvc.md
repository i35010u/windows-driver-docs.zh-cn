---
title: UVC 中的红外流支持
description: 提供有关 UVC 中的红外流支持的信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 512b58a817cc4efe95a4d48b8bc3d28a1d0ffcfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576532"
---
# <a name="infrared-stream-support-in-uvc"></a>UVC 中的红外流支持

在 Windows 10，版本 1607年及更高版本中的收件箱 USB 视频类 (UVC) 驱动程序支持生成红外 (IR) 流的摄像头。 

这些相机捕获场景的亮度值，并通过 USB 传输这些帧未压缩的格式为或压缩的 MJPEG 格式。 通过媒体捕获管道的应用程序获知这些相机和其流。 

以下的红外线 （ir） 格式类型 Guid 用于指定流的视频格式说明符，以便应用程序正确获知红外线 （ir） 流。

Ksmedia.h 中定义了这些红外线 （ir） 格式类型 Guid:

| 红外线 （ir） 格式类型 GUID             | 描述                          |
|---------------------------------|--------------------------------------|
| KSDATAFORMAT_SUBTYPE_L8_IR      | 8 位仅限亮度的帧               |
| KSDATAFORMAT_SUBTYPE_L16_IR     | 16 位仅限亮度的帧              |
| KSDATAFORMAT_SUBTYPE_MJPEG_IR   | 压缩的 MJPEG 仅限亮度的帧    |

如果指定了这些红外线 （ir） 格式类型的 Guid，捕获管道自动将这些流标记为红外线 （ir） 流，从而提供帮助选择适合其正确的流中的应用程序。

```cpp
// Example: Format descriptor for UVC 1.1 frame based uncompressed format

typedef struct _VIDEO_FORMAT_FRAME
{
    UCHAR bLength;
    UCHAR bDescriptorType;
    UCHAR bDescriptorSubtype;
    UCHAR bFormatIndex;
    UCHAR bNumFrameDescriptors;
    GUID  guidFormat;           // guidFormat must contain one of the IIR format type GUIDs from the table above
    UCHAR bBitsPerPixel;
    UCHAR bDefaultFrameIndex;
    UCHAR bAspectRatioX;
    UCHAR bAspectRatioY;
    UCHAR bmInterlaceFlags;
    UCHAR bCopyProtect;
    UCHAR bVariableSize;
} VIDEO_FORMAT_FRAME, *PVIDEO_FORMAT_FRAME;
```





