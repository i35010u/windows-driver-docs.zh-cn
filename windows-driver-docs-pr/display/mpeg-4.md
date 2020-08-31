---
title: MPEG-4
description: MPEG-4
ms.assetid: 7879acd5-39fe-46b4-a427-43e4ea52315e
keywords:
- MPEG-2 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ed4496697e3be3964e9cc8507451c41526604fe
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066488"
---
# <a name="mpeg-4"></a>MPEG-4


## <span id="ddk_mpeg_4_gg"></span><span id="DDK_MPEG_4_GG"></span>


MPEG-2 基于 .H 进行渐进式扫描编码，而在 MPEG-2 上基于4:2:0 的隔行扫描和颜色采样格式支持。 支持 mpeg-2 和 MPEG-2 功能的功能可用于支持 mpeg-2。

MPEG-2 可支持大于8位的示例准确性。 DirectX VA 包含一种机制，该机制使用[**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的**bBPPminus1**成员支持每个像素超过8位。

**注意**   DirectX VA 不支持最独特的 MPEG-2 功能，如形状编码、对象方向、人脸建模、网格对象和子画面。

 

 

