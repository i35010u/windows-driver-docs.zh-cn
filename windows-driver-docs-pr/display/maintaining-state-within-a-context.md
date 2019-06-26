---
title: 维护上下文中的状态
description: 维护上下文中的状态
ms.assetid: dabf6aa7-f127-419c-9245-5270768fef5b
keywords:
- 上下文 WDK Direct3D 维护状态
- 指出 WDK Direct3D
- 内部状态 WDK Direct3D
- 公共状态 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5cc972ad7a527ba9bfaa847fec6f93535d2b9c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379023"
---
# <a name="maintaining-state-within-a-context"></a>维护上下文中的状态


## <span id="ddk_maintaining_state_within_a_context_gg"></span><span id="DDK_MAINTAINING_STATE_WITHIN_A_CONTEXT_GG"></span>


驱动程序更新与上下文关联其内部状态时其[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)调用回调。 此回调还必须在 Direct3D 中返回更新后的上下文公共状态。

 

 





