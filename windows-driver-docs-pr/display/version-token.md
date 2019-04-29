---
title: 版本标记
description: 版本标记
ms.assetid: e38ae148-3bb8-41b4-acdd-55bd67c24d48
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 663a895f6c234d8265e4295b6110b119a69377cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390764"
---
# <a name="version-token"></a>版本标记


## <span id="ddk_version_token_gg"></span><span id="DDK_VERSION_TOKEN_GG"></span>


版本标记描述的着色器代码的版本号，并告知驱动程序的着色器代码是否用于像素或顶点着色器。 版本标记组成以下位：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_07_00_"></span>**\[07:00\]**  0 到 7 位指示的次版本号或代码。

<span id="_15_08_"></span>**\[15:08\]** 位 8 到 15 指定的主版本号或代码。

<span id="_31_16_"></span>**\[31:16\]** 到 31 位 16 指定代码是否为像素或顶点着色器。
像素着色器，对于值为 0xFFFF。
对于顶点着色器，值为 0xFFFE。
## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





