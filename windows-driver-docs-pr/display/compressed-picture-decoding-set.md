---
title: 压缩图片解码集
description: 压缩图片解码集
ms.assetid: 7d6e2050-663e-4370-a210-1d319cfbde6d
keywords:
- 压缩的图片解码设置 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b424a8d684218e72632aae2a7c08689a103dcb2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065264"
---
# <a name="compressed-picture-decoding-set"></a>压缩图片解码集


## <span id="ddk_compressed_picture_decoding_set_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_SET_GG"></span>


此部分定义压缩图片解码的最小互操作性配置集。 此整套配置必须受解码器支持，并且加速器必须支持此集内的一个或多个配置。 提供了一个 [额外的配置集](additional-encouraged-configuration-set.md) ，建议 (这些配置不需要) 。

此集中的前六个配置适用于所有 [受限制的配置文件](restricted-profiles.md)。 此集中的第七个配置仅针对 MPEG2 \_ C 和 mpeg2 \_ D 定义。

压缩图片解码配置的最小互操作性配置集是由第三个到 [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode) 结构的最后一个成员定义的。

 

