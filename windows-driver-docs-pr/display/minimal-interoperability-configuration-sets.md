---
title: 最低互操作性配置集
description: 最低互操作性配置集
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，受限制的配置文件
- 视频加速 WDK DirectX，受限配置文件
- VA WDK DirectX，受限配置文件
- 受限配置文件 WDK DirectX VA
- 最小互操作性配置集 WDK DirectX VA
- 互操作性配置集 WDK DirectX VA
- 配置集 WDK DirectX VA
- DXVA_ConfigPictureDecode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b61c08baa8f0cf9faec958cf859c7f30613d2d7a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822461"
---
# <a name="minimal-interoperability-configuration-sets"></a>最低互操作性配置集


## <span id="ddk_minimal_interoperability_configuration_sets_gg"></span><span id="DDK_MINIMAL_INTEROPERABILITY_CONFIGURATION_SETS_GG"></span>


所有 DirectX VA 解码器都必须使用所有 DirectX VA 加速器运行，才能使用 [受限制的配置文件](restricted-profiles.md)。 每个解码器都必须能够与一组连接配置的任何成员进行操作，并且每个加速器都必须能够操作至少有一个该集的成员。 有三个配置集用于定义设备驱动程序必须提供的最小级别的功能：

[压缩图片解码集](compressed-picture-decoding-set.md)

[Alpha 混合数据加载集](alpha-blend-data-loading-set.md)

[Alpha 混合组合集](alpha-blend-combination-set.md)

对于每个设置，解码器和加速器必须支持相同的 DirectX VA 限制模式 GUID。

 

 





