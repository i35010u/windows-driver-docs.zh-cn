---
title: 压缩图片解码集
description: 压缩图片解码集
ms.assetid: 7d6e2050-663e-4370-a210-1d319cfbde6d
keywords:
- 压缩的图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98d7722f4ab076d24f86a239dd95e2222012dc31
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839797"
---
# <a name="compressed-picture-decoding-set"></a>压缩图片解码集


## <span id="ddk_compressed_picture_decoding_set_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_SET_GG"></span>


此部分定义压缩图片解码的最小互操作性配置集。 此整套配置必须受解码器支持，并且加速器必须支持此集内的一个或多个配置。 提供了一个[附加的配置集](additional-encouraged-configuration-set.md)，建议为其提供支持（不需要这些配置）。

此集中的前六个配置适用于所有[受限制的配置文件](restricted-profiles.md)。 此集中的第七个配置仅为 MPEG2\_C 和 MPEG2\_D 定义。

压缩图片解码配置的最小互操作性配置集是由第三个到[**DXVA\_ConfigPictureDecode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的最后一个成员定义的。

 

 





