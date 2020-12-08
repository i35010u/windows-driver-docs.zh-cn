---
title: MPEG-4
description: MPEG-4
keywords:
- MPEG-2 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c8990731ecc2fc219e155e5152dc560f4299101
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836519"
---
# <a name="mpeg-4"></a>MPEG-4


## <span id="ddk_mpeg_4_gg"></span><span id="DDK_MPEG_4_GG"></span>


MPEG-2 基于 .H 进行渐进式扫描编码，而在 MPEG-2 上基于4:2:0 的隔行扫描和颜色采样格式支持。 支持 mpeg-2 和 MPEG-2 功能的功能可用于支持 mpeg-2。

MPEG-2 可支持大于8位的示例准确性。 DirectX VA 包含一种机制，该机制使用 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bBPPminus1** 成员支持每个像素超过8位。

**注意**   DirectX VA 不支持最独特的 MPEG-2 功能，如形状编码、对象方向、人脸建模、网格对象和子画面。

 

 

