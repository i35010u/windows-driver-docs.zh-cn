---
title: 压缩的图片解码
description: 压缩的图片解码
ms.assetid: 61633a15-72e4-49a4-9a42-684bde21df9e
keywords:
- 压缩解码 WDK DirectX VA 的图片
- 图片解码 WDK DirectX VA，压缩
- 视频解码 WDK DirectX VA，压缩的图片
- 解码视频 WDK DirectX VA，压缩图片
- 有关解码 WDK DirectX VA，压缩的图片压缩图片解码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dca118023d2e0cd49c5d0f23d4db0979d56a8a88
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545587"
---
# <a name="compressed-picture-decoding"></a>压缩的图片解码


## <span id="ddk_compressed_picture_decoding_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_GG"></span>


当[bDXVA\_Func 变量](bdxva-func-variable.md)等于 1，指定压缩的图片解码操作。 [ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构包含压缩的图片解码的 DirectX VA 连接配置数据。

### <a name="span-idcompressedpictureparametersspanspan-idcompressedpictureparametersspanspan-idcompressedpictureparametersspancompressed-picture-parameters"></a><span id="Compressed_Picture_Parameters"></span><span id="compressed_picture_parameters"></span><span id="COMPRESSED_PICTURE_PARAMETERS"></span>压缩的图片参数

必须一次发送每个图片要解码的参数中指定[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构。

 

 





