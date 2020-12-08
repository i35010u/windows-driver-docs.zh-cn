---
title: WIA 原始数据标头
description: WIA 原始数据标头
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a07cd1ff8bd2b807b6a8360823a6ad4291b27bc3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826461"
---
# <a name="wia-raw-data-header"></a>WIA 原始数据标头


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

<a href="" id="dword-compression"></a>DWORD *压缩*  
允许压缩的原始格式，如 Nikon 的压缩 NEF 和 headerless 压缩的数据，用于压缩的传真传输 (组3.1、3.2 d、4) 。 此字段的值将为 WIA \_ IPA \_ 压缩常量，可能是特定于供应商的特定应用程序。 默认值为 WIA \_ 压缩 \_ NONE。

压缩示例：

G4 压缩的数据 (WIA \_ 压缩 \_ G4) 可以在 tiff 文件中传输 (WiaImgFmt \_ tiff) 或使用原始格式 (WiaImgFmt \_ raw) 。

JPEG 压缩数据 (WIA \_ 压缩 \_ jpeg) 可使用 JFIF 格式传输 (WiaImgFmt \_ JPEG) 、EEXIF 格式 (WiaImgFmt \_ EXIF) 或 TIFF 格式 (WiaImgFmt \_ tiff) 。 使用原始格式 (WiaImgFmt raw) ，不能以其中一种交换格式传输 JPEG 数据 (JFIF，EEXIF) ， \_ 而是必须使用其他与 JPEG 兼容的格式之一。

有关 WIA 压缩常量的详细信息，请参阅 [**wia \_ IPA \_ compression**](./wia-ipa-compression.md) 属性。

<a href="" id="dword-photometricinterp"></a>DWORD *PhotometricInterp*  
描述传输的图像的 photometric 解释。 此字段对于黑白 (1bpp) 和灰度 (4bpp 或更多) 图像是必需的。 这些图像需要指示白色和黑色的值、WIA \_ 照片 \_ \_ 1 (其中白色为1，黑色为 0) 或 WIA \_ 照片 \_ \_ 0 (，其中白色为0，黑色为 1) 。 对于彩色图像，此字段是可选的。

<a href="" id="dword-lineorder"></a>DWORD *LineOrder*  
描述图像数据中的行/行是从上到下还是从下到上排序。 为此，在 *wiadef* 中定义了两个新常量：

```cpp
#define  WIA_LINE_ORDER_TOP_TO_BOTTOM        0x00000001 
#define  WIA_LINE_ORDER_BOTTOM_TO_TOP        0x00000002
```

没有为此定义的新属性。 这不是一个可配置的扫描设置。 *LingOrder* 仅在执行图像数据传输时才有意义。

<a href="" id="dword-rawdatasize"></a>DWORD *RawDataSize*  
指示标头后的原始数据的大小（以字节为单位） (不包括可选调色板) 。 应用程序可以使用此字段来验证是否已完成假设的成功图像传输。 当传输开始 (且标头写入到) 流时，此信息对微型驱动程序而言是未知的（例如，当使用自动边框检测来扫描图像时），微型驱动程序应需要在图像数据传输的末尾填写此字段，类似于 XExtent 和 YExtent 字段的处理方式。

<a href="" id="dword-paletteoffset"></a>DWORD *PaletteOffset*  
包含调色板在数据流中的起始位置的偏移量（以字节为单位）;此偏移量在标头结束的位置零) 开始 (。 调色板和原始图像数据可以按任意顺序跟踪原始标头，并且在不需要时可以省略调色板。

<a href="" id="dword-palettesize"></a>DWORD *PaletteSize*  
包含调色板的大小（以字节为单位）。 当不需要将调色板附加到原始图像数据时，微型驱动程序应将此字段设置为0。 此字段与调色板中的条目数无关。

黑白数据和灰度数据可以省略调色板 (因为生成调色板所需的信息) 包含在 *PhotometricInterpretation* 字段中，或者提供优化调色板和 *PhotometricInterpretation* 字段。

对于索引图像，调色板中的条目数由当前 *ysteminfo.displaysettings.bitsperpixel* 值决定 (2 ^ *ysteminfo.displaysettings.bitsperpixel*。 例如，两个条目用于1bpp，16个条目用于4bpp，256项用于 8bpp) 。 调色板项的格式将由 " *BitsPerChannel* " 字段中的条目数来决定 (每个调色板条目中的字段/通道数) 和 *BitsPerChannel* 值 (每个字段都将包含在各自通道) 的 *BitsPerChannel* 字段中指定的值。 每个调色板输入字段必须按字节对齐。

 

