---
title: 维护上下文中的状态
description: 维护上下文中的状态
keywords:
- 上下文 WDK Direct3D，维护状态
- 状态 WDK Direct3D
- 内部状态 WDK Direct3D
- 公共状态 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3c7e48ccc8e177a49822133f4f408c2b8f841f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793927"
---
# <a name="maintaining-state-within-a-context"></a>维护上下文中的状态


## <span id="ddk_maintaining_state_within_a_context_gg"></span><span id="DDK_MAINTAINING_STATE_WITHIN_A_CONTEXT_GG"></span>


在调用 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 回调时，驱动程序将更新与上下文关联的内部状态。 此回调还必须将更新的上下文的公共状态返回到 Direct3D。

 

