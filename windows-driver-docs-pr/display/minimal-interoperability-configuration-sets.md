---
title: 最低互操作性配置集
description: 最低互操作性配置集
ms.assetid: 2390c710-8693-4af4-903f-89068436141d
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，受限制的配置文件
- 视频加速 WDK DirectX，受限制的配置文件
- VA WDK DirectX，受限制的配置文件
- 受限制的配置文件 WDK DirectX VA
- 最小互操作性配置设置 WDK DirectX VA
- 互操作性配置设置 WDK DirectX VA
- 配置设置 WDK DirectX VA
- DXVA_ConfigPictureDecode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac5c3548e2f3930f3dcc1f7b5cb323fe6c46a6fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385032"
---
# <a name="minimal-interoperability-configuration-sets"></a>最低互操作性配置集


## <span id="ddk_minimal_interoperability_configuration_sets_gg"></span><span id="DDK_MINIMAL_INTEROPERABILITY_CONFIGURATION_SETS_GG"></span>


所有 DirectX VA 解码器必须都运行与所有要使用的 DirectX VA 加速器[受限制的配置文件](restricted-profiles.md)。 使用一组连接配置的任何成员的每个解码器必须是支持的操作和每个加速器必须能够与至少一个成员，该集的操作。 有三个定义最小的设备驱动程序必须提供的功能级别的配置集：

[压缩解码集的图片](compressed-picture-decoding-set.md)

[Alpha 混合数据加载组](alpha-blend-data-loading-set.md)

[Alpha 混合组合集](alpha-blend-combination-set.md)

每个设置解码器和快捷键必须支持 DirectX VA 受限制的模式 GUID 相同。

 

 





