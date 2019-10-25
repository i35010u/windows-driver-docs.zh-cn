---
title: 维护上下文中的状态
description: 维护上下文中的状态
ms.assetid: dabf6aa7-f127-419c-9245-5270768fef5b
keywords:
- 上下文 WDK Direct3D，维护状态
- 状态 WDK Direct3D
- 内部状态 WDK Direct3D
- 公共状态 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0699f6248b2936acdfa7ba9547d5d56260bf02ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840586"
---
# <a name="maintaining-state-within-a-context"></a>维护上下文中的状态


## <span id="ddk_maintaining_state_within_a_context_gg"></span><span id="DDK_MAINTAINING_STATE_WITHIN_A_CONTEXT_GG"></span>


在调用[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)回调时，驱动程序将更新与上下文关联的内部状态。 此回调还必须将更新的上下文的公共状态返回到 Direct3D。

 

 





