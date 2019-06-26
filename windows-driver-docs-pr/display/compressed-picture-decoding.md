---
title: 压缩图片解码
description: 压缩图片解码
ms.assetid: 61633a15-72e4-49a4-9a42-684bde21df9e
keywords:
- 压缩解码 WDK DirectX VA 的图片
- 图片解码 WDK DirectX VA，压缩
- 视频解码 WDK DirectX VA，压缩的图片
- 解码视频 WDK DirectX VA，压缩图片
- 有关解码 WDK DirectX VA，压缩的图片压缩图片解码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eef9b36d575a36b76e6d74c60f83cd92f56a363
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370666"
---
# <a name="compressed-picture-decoding"></a>压缩图片解码


## <span id="ddk_compressed_picture_decoding_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_GG"></span>


当[bDXVA\_Func 变量](bdxva-func-variable.md)等于 1，指定压缩的图片解码操作。 [ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)结构包含压缩的图片解码的 DirectX VA 连接配置数据。

### <a name="span-idcompressedpictureparametersspanspan-idcompressedpictureparametersspanspan-idcompressedpictureparametersspancompressed-picture-parameters"></a><span id="Compressed_Picture_Parameters"></span><span id="compressed_picture_parameters"></span><span id="COMPRESSED_PICTURE_PARAMETERS"></span>压缩的图片参数

必须一次发送每个图片要解码的参数中指定[ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)结构。

 

 





