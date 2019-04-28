---
title: 注释标记
description: 注释标记
ms.assetid: b1e5f8c8-4d7d-49ce-876d-4a6cbccc550d
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0fb8573358d38a3a7621bfbb336dc5709f2c4a35
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342989"
---
# <a name="comment-token"></a>注释标记


## <span id="ddk_comment_token_gg"></span><span id="DDK_COMMENT_TOKEN_GG"></span>


注释标记描述了注释的遵循，且由以下位的长度：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_15_00_"></span>**\[15:00\]**  0 到 15 位指示该令牌是否注释标记。 此值是 0xFFFE。

<span id="_30_16_"></span>**\[30:16\]** 位 16 至 30 注释后面的 dword 值中指定的长度。 注释可以最大为 2 ^15 dword 值的长度，等于 128 KB 的视频内存或系统内存。

<span id="_31_"></span>**\[31\]** 位 31 是零 (0x0)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

请注意，dword 值的第 31 位后面的注释中不需要设置为 0x1。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





