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
ms.openlocfilehash: 80d688d1dfbbbe09b2b2cc5c20dbb2d185879218
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525413"
---
# <a name="maintaining-state-within-a-context"></a>维护上下文中的状态


## <span id="ddk_maintaining_state_within_a_context_gg"></span><span id="DDK_MAINTAINING_STATE_WITHIN_A_CONTEXT_GG"></span>


驱动程序更新与上下文关联其内部状态时其[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)调用回调。 此回调还必须在 Direct3D 中返回更新后的上下文公共状态。

 

 





