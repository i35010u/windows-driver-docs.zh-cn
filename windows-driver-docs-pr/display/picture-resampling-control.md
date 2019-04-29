---
title: 画面重新采样控制
description: 画面重新采样控制
ms.assetid: 08d74812-3393-4461-91c4-644ecc5ad428
keywords:
- 重新采样 WDK DirectX VA 的图片
- 空间可缩放的视频编码 WDK DirectX VA
- 引用图片来重新采样 WDK DirectX VA
- 重新采样图片 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b2309eb3ae18e3c3654356e66f939ea62513b30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352220"
---
# <a name="picture-resampling-control"></a>画面重新采样控制


## <span id="ddk_picture_resampling_control_gg"></span><span id="DDK_PICTURE_RESAMPLING_CONTROL_GG"></span>


当[bDXVA\_Func 变量](bdxva-func-variable.md)是等于 4，该操作指定为图片来重新采样。 此操作用于目的，例如空间可缩放的视频编码，引用图片来重新采样，或为重新采样用作采样或显示图片。

图片来重新采样执行 H.263 Annex O 空间可伸缩性或 H.263 Annex P 中使用指定的图片两端的剪辑，这是图片来重新采样如某些形式的 mpeg-2 和 MPEG 4 中的空间可伸缩性中所示的相同方法。 此函数使用简单双点击可分离筛选。

请注意该图片来重新采样控件不需要连接配置。 其操作需要仅支持相应受限模式下的 GUID。 无连接需进行配置以图片来重新采样控件，因为没有最小互操作性集必须定义进行其操作。

中的单个缓冲区类型定义[ **DXVA\_PicResample** ](https://msdn.microsoft.com/library/windows/hardware/ff564010)结构控制重新采样过程。

 

 





