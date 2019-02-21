---
title: WIA 的原始数据标头
description: WIA 的原始数据标头
ms.assetid: a2cb3835-7879-4f69-9784-9487df40730a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f90e4a9bef3e2d0655498515c25b519d6e4e02f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555484"
---
# <a name="wia-raw-data-header"></a>WIA 的原始数据标头


原始数据的标头如下所示：

```cpp
DWORD Tag;         // must contain 'WRAW' (single byte ASCII characters)
DWORD Version;        // must contain 0x00010000
DWORD HeaderSize;       // contains amount of valid bytes in header
DWORD XRes;              // X (horizontal) resolution, in DPI
DWORD YRes;              // Y (vertical) resolution, in DPI
DWORD XExtent;           // image width, in pixels
DWORD YExtent;           // image height, in pixels
DWORD BytesPerLine;      // used only for uncompressed image data, 0 (unknown) for compressed data 
DWORD BitsPerPixel;      // number of bits per pixel (all channels)
DWORD ChannelsPerPixel;  // number of color channels (samples) within a pixel
DWORD DataType;    // current WIA_IPA_DATATYPE value describing the image
BYTE  BitsPerChannel[8]; // up to 8 channels per pixel, use as many as needed  
DWORD Compression;       // current WIA_IPA_COMPRESSION value
DWORD PhotometricInterp; // current WIA_IPS_PHOTOMETRIC_INTERP value
DWORD LineOrder;         // image line order as a WIA_LINE_ORDER value
DWORD RawDataOffset;     // offset position (in bytes, starting from 0) for the raw image data
DWORD RawDataSize;       // size of raw image data, in bytes
DWORD PaletteOffset;     // offset position (in bytes, starting from 0) for the palette (0 if none)
DWORD PaletteSize;       // size, in bytes, of color palette table (0 if no palette is required) 
```

### <a name="additional-header-field-descriptions"></a>其他标头字段说明

<a href="" id="dword-compression"></a>DWORD*压缩*  
允许压缩的原始格式，如上市的 Nikon 的压缩的 NEF 和 headerless 压缩的传真传输 (组 3.1，3.2d，4) 所用的压缩的数据。 值此字段将是 WIA\_IPA\_压缩常量，可能是供应商特定的专用应用程序。 默认值是 WIA\_压缩\_NONE。

压缩示例：

G4 压缩数据 (WIA\_压缩\_G4) 可能会传输 TIFF 文件中 (WiaImgFmt\_TIFF) 或使用原始格式 (WiaImgFmt\_RAW)。

JPEG 压缩数据 (WIA\_压缩\_JPEG) 无法使用 JFIF 格式传输 (WiaImgFmt\_JPEG)，EEXIF 格式 (WiaImgFmt\_EXIF)，或 TIFF 格式 (WiaImgFmt\_TIFF). 不能传输 JPEG 数据交换格式之一 （JFIF、 EEXIF） 中使用原始格式的传输格式 (WiaImgFmt\_RAW)-而是必须使用其他 JPEG 兼容格式之一。

WIA 压缩常量的详细信息，请参阅[ **WIA\_IPA\_压缩**](https://msdn.microsoft.com/library/windows/hardware/ff551540)属性。

<a href="" id="dword-photometricinterp"></a>DWORD *PhotometricInterp*  
介绍传输图像测光解释。 此字段是黑色和白色 (1bpp) 和 （4bpp 或以上） 的灰度图像所必需的。 这些映像需要指示的值为白色和黑色，任一 WIA\_照片\_白色\_1 (其中白色为 1，黑色，则为 0) 或 WIA\_照片\_白色\_0 (其中白色，则为 0，黑色为 1)。 此字段是可选的彩色图像。

<a href="" id="dword-lineorder"></a>DWORD *LineOrder*  
介绍顶部到底部或下到上是否已排序的行中的图像数据。 在中定义的两个新常量*wiadef.h*此：

```cpp
#define  WIA_LINE_ORDER_TOP_TO_BOTTOM        0x00000001 
#define  WIA_LINE_ORDER_BOTTOM_TO_TOP        0x00000002
```

没有为此定义新属性。 这不是可配置的扫描设置。 *LingOrder*仅相关问题时执行图像数据传输。

<a href="" id="dword-rawdatasize"></a>DWORD *RawDataSize*  
指示大小 （字节） 之后 （不包括可选的调色板） 的标头的原始数据。 应用程序可以使用此字段来验证假定成功图像传输完成。 此信息时是未知的微型驱动程序时开始进行转移 （和标头写入到流）-例如时使用自动边框检测扫描图像-微型驱动程序应该需要填写此字段末尾的 image 数据传输，类似于如何处理大 XExtent 和 YExtent 字段。

<a href="" id="dword-paletteoffset"></a>DWORD *PaletteOffset*  
包含的偏移量，以字节为单位的颜色调色板数据流; 中的开始位置此偏移量 （是同时开始的位置零） 标头的结束位置... 调色板和原始图像数据可以按照任意顺序中的原始标头，不需要时可以省略调色板。

<a href="" id="dword-palettesize"></a>DWORD *PaletteSize*  
包含的大小，以字节为单位的调色板。 当需要附加到原始图像数据时没有调色板时，微型驱动程序应将此字段设置为 0。 此字段不相关的调色板中的条目数。

黑色和白色和灰度数据可省略调色板 (因为构建控制板所需的信息包含在*PhotometricInterpretation*字段)，或提供与优化的调色板*PhotometricInterpretation*字段。

对于索引映像，调色板中的条目数由当前*BitsPerPixel*值 (2 ^ *BitsPerPixel*。 例如，2 个条目 1bpp、 16 个条目为 4bpp、 256 8bpp 条目）。 中的条目数将取决于调色板条目的格式*BitsPerChannel*字段 （字段/通道中的每个调色板条目数） 和*BitsPerChannel* （每个字段将的值包含值中指定完全*BitsPerChannel*字段为各自的通道)。 调色板条目的每个字段必须是字节对齐。

 

 




