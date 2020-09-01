---
title: 压缩图片解码
description: 压缩图片解码
ms.assetid: 61633a15-72e4-49a4-9a42-684bde21df9e
keywords:
- 压缩的图片解码 WDK DirectX VA
- 图片解码 WDK DirectX VA，已压缩
- 视频解码 WDK DirectX VA，压缩图片
- 解码视频 WDK DirectX VA，压缩图片
- 压缩的图片解码 WDK DirectX VA，关于压缩图片解码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c3f8ec088e8f7a33af42bf88b93e3481a17de3e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064912"
---
# <a name="compressed-picture-decoding"></a>压缩图片解码


## <span id="ddk_compressed_picture_decoding_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_GG"></span>


当 [bDXVA \_ Func 变量](bdxva-func-variable.md) 等于1时，指定的操作是压缩图片解码。 [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构包含用于压缩的图片解码的 DirectX VA 连接配置数据。

### <a name="span-idcompressed_picture_parametersspanspan-idcompressed_picture_parametersspanspan-idcompressed_picture_parametersspancompressed-picture-parameters"></a><span id="Compressed_Picture_Parameters"></span><span id="compressed_picture_parameters"></span><span id="COMPRESSED_PICTURE_PARAMETERS"></span>压缩图片参数

在 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters) 结构中指定了一次为每个要解码的图片发送的参数。

 

