---
title: 画面重新采样控制
description: 画面重新采样控制
keywords:
- 图片重新采样 WDK DirectX VA
- 空间可伸缩视频编码 WDK DirectX VA
- 参考图片重新采样 WDK DirectX VA
- 重新采样图片 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cec24da4a7cbd9fc47a731c29d2eb47aff69c3ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838055"
---
# <a name="picture-resampling-control"></a>画面重新采样控制


## <span id="ddk_picture_resampling_control_gg"></span><span id="DDK_PICTURE_RESAMPLING_CONTROL_GG"></span>


当 [bDXVA \_ Func 变量](bdxva-func-variable.md) 等于4时，指定的操作是图片重新采样。 此操作用于实现空间可伸缩的视频编码、引用图片的重新采样或重新采样，以用作 upsampled 或显示图片。

图片重新采样按照在中指定的方法执行，如在 H-p 附录 O 空间可伸缩性中指定，或者在以图片边缘进行剪辑的 H-p 附录 P 中执行，这与在 MPEG-2 和 MPEG-2 的某些形式的空间可伸缩性中一样，这种方法的重新采样方法相同。 此函数使用简单的双点击分离筛选。

请注意，图片重新采样控制不需要连接配置。 其操作只需要支持相应的受限模式 GUID。 由于图像重新采样控制不需要连接配置，因此不能为其操作定义最小互操作性集。

在 [**DXVA \_ PicResample**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_picresample) 结构中定义的单个缓冲区类型控制重新采样进程。

 

