---
title: 版本标记
description: 版本标记
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d18a07be9dc3c6d4550c1fcd7f1fc75bab2d8d91
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798249"
---
# <a name="version-token"></a>版本标记


## <span id="ddk_version_token_gg"></span><span id="DDK_VERSION_TOKEN_GG"></span>


版本标记描述着色器代码的版本号，并通知驱动程序着色器代码是用于像素着色器还是顶点着色器。 版本令牌由以下位组成：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>带宽

<span id="_07_00_"></span>**\[ 07:00 \]** 位0到7指示次版本号或代码。

<span id="_15_08_"></span>**\[ 15:08 \]** 位8到15指定主要版本号或代码。

<span id="_31_16_"></span>**\[ 31:16 \]** 位16到31指定代码是用于像素着色器还是用于顶点着色器。
对于像素着色器，该值为0xFFFF。
对于顶点着色器，值为0xFFFE。
## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





