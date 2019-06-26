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
- 解码 WDK DirectX va，因此格式的图片
- 格式 WDK DirectX VA
- 图片解码 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9b00f5c86a682745c2a1c853b57710c668d233a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365520"
---
# <a name="setting-up-directx-va-decoding"></a>设置 DirectX VA 解码


## <span id="ddk_setting_up_directx_va_decoding_gg"></span><span id="DDK_SETTING_UP_DIRECTX_VA_DECODING_GG"></span>


为了使解码器才能正常使用加速器，解码器和快捷键必须设置为两个不同方面的操作：

-   要解码的视频数据的格式。 [ **DXVA\_ConnectMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_connectmode)结构用于指定的格式。

-   确定格式用于主机和加速器之间交换数据和建立哪个进程所在的主机和该快捷键上配置。 此配置建立的连接配置为每个 DirectX VA 函数要使用的协商 (由[bDXVA\_Func](bdxva-func-variable.md)变量)。 [ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)结构指定的配置。

 

 





