---
title: 压缩解码集的图片
description: 压缩解码集的图片
ms.assetid: 7d6e2050-663e-4370-a210-1d319cfbde6d
keywords:
- 压缩解码集 WDK DirectX VA 的图片
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d556a2cb35dd002155f0d74dbbce0f90d04c322e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521444"
---
# <a name="compressed-picture-decoding-set"></a>压缩解码集的图片


## <span id="ddk_compressed_picture_decoding_set_gg"></span><span id="DDK_COMPRESSED_PICTURE_DECODING_SET_GG"></span>


本部分将定义为压缩的图片解码设置的最小互操作性配置。 解码器，必须支持此整个配置集和快捷键必须支持此集中的一个或多个配置。 [额外的配置集](additional-encouraged-configuration-set.md)提供有关建议的支持 （这些配置不是必需的）。

在此集中的前六个配置适用于所有[受限制的配置文件](restricted-profiles.md)。 在此集中的第七个配置定义仅为 MPEG2\_C 和 MPEG2\_d。

由第三到的最后一个成员定义的最小互操作性配置集中的配置用于压缩的图片解码[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构。

 

 





