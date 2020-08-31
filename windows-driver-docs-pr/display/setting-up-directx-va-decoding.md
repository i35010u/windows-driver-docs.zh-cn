---
title: 设置 DirectX VA 解码
description: 设置 DirectX VA 解码
ms.assetid: 8841c366-df00-4e88-9f50-85345ba77e03
keywords:
- 视频解码 WDK DirectX VA，设置
- 解码视频 WDK DirectX VA，设置
- 图片解码 WDK DirectX VA，设置
- 视频解码 WDK DirectX VA，格式
- 解码视频 WDK DirectX VA，格式
- 图片解码 WDK DirectX VA，格式
- 格式化 WDK DirectX VA
- 图片解码 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f26f142f48dab1b4f2ba8bc803fcc6fb7b5eb160
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063467"
---
# <a name="setting-up-directx-va-decoding"></a>设置 DirectX VA 解码


## <span id="ddk_setting_up_directx_va_decoding_gg"></span><span id="DDK_SETTING_UP_DIRECTX_VA_DECODING_GG"></span>


为了使解码器正确操作加速器，必须为操作的两个不同方面设置解码器和加速器：

-   要解码的视频数据的格式。 [**DXVA \_ ConnectMode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)结构用于指定格式。

-   用于确定主机和加速器之间用于数据交换的格式的配置，并确定哪个进程驻留在主机上以及在加速器上。 此配置是通过协商每个 DirectX VA 函数的连接配置而建立的， (由 [bDXVA \_ Func](bdxva-func-variable.md) 变量) 确定。 [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构指定配置。

 

