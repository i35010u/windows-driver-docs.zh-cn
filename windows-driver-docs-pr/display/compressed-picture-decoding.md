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
ms.openlocfilehash: 20dd82a811b90a1b7a9d7a25577bf0db1fd6dea6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839048"
---
# <a name="compressed-picture-decoding"></a>压缩图片解码


## <span id="ddk_compressed_picture_decoding_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_GG"></span>


当[bDXVA\_Func 变量](bdxva-func-variable.md)等于1时，指定的操作是压缩图片解码。 [**DXVA\_ConfigPictureDecode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构包含用于压缩的图片解码的 DirectX VA 连接配置数据。

### <a name="span-idcompressed_picture_parametersspanspan-idcompressed_picture_parametersspanspan-idcompressed_picture_parametersspancompressed-picture-parameters"></a><span id="Compressed_Picture_Parameters"></span><span id="compressed_picture_parameters"></span><span id="COMPRESSED_PICTURE_PARAMETERS"></span>压缩图片参数

对于要解码的每个图片，必须发送一次的参数在[**DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构中指定。

 

 





