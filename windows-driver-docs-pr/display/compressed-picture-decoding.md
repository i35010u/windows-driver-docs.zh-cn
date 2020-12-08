---
title: 压缩图片解码
description: 压缩图片解码
keywords:
- 压缩的图片解码 WDK DirectX VA
- 图片解码 WDK DirectX VA，已压缩
- 视频解码 WDK DirectX VA，压缩图片
- 解码视频 WDK DirectX VA，压缩图片
- 压缩的图片解码 WDK DirectX VA，关于压缩图片解码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7eb72c6d1e0efd748b5060ca975700227bc7a204
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810217"
---
# <a name="compressed-picture-decoding"></a>压缩图片解码


## <span id="ddk_compressed_picture_decoding_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_GG"></span>


当 [bDXVA \_ Func 变量](bdxva-func-variable.md) 等于1时，指定的操作是压缩图片解码。 [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构包含用于压缩的图片解码的 DirectX VA 连接配置数据。

### <a name="span-idcompressed_picture_parametersspanspan-idcompressed_picture_parametersspanspan-idcompressed_picture_parametersspancompressed-picture-parameters"></a><span id="Compressed_Picture_Parameters"></span><span id="compressed_picture_parameters"></span><span id="COMPRESSED_PICTURE_PARAMETERS"></span>压缩图片参数

在 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters) 结构中指定了一次为每个要解码的图片发送的参数。

 

