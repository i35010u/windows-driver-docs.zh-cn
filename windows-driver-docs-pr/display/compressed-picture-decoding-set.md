---
title: 压缩图片解码集
description: 压缩图片解码集
keywords:
- 压缩的图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41e8bf08cdfcfdc4f40eb706f96a9f8946de527a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810219"
---
# <a name="compressed-picture-decoding-set"></a>压缩图片解码集


## <span id="ddk_compressed_picture_decoding_set_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_SET_GG"></span>


此部分定义压缩图片解码的最小互操作性配置集。 此整套配置必须受解码器支持，并且加速器必须支持此集内的一个或多个配置。 提供了一个 [额外的配置集](additional-encouraged-configuration-set.md) ，建议 (这些配置不需要) 。

此集中的前六个配置适用于所有 [受限制的配置文件](restricted-profiles.md)。 此集中的第七个配置仅针对 MPEG2 \_ C 和 mpeg2 \_ D 定义。

压缩图片解码配置的最小互操作性配置集是由第三个到 [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode) 结构的最后一个成员定义的。

 

