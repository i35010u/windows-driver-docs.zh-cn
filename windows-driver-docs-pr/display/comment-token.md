---
title: 注释标记
description: 注释标记
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 327cf41c9406136ef67950d75fe90cb42095d21e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810249"
---
# <a name="comment-token"></a>注释标记


## <span id="ddk_comment_token_gg"></span><span id="DDK_COMMENT_TOKEN_GG"></span>


注释标记描述了后面的注释长度，并且由以下位组成：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>带宽

<span id="_15_00_"></span>**\[ 15:00 \]** 位0到15表示该令牌是注释令牌。 此值为0xFFFE。

<span id="_30_16_"></span>**\[ 30:16 \]** 位16到30指定其后注释的 dword 长度。 注释最多可包含 2 ^ 15 个 Dword，长度为 128 KB 的视频内存或系统内存。

<span id="_31_"></span>**\[ 31 \]** 位31为零 (0x0) 。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

请注意，下面注释中的 Dword 的31位不需要设置为0x1。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





