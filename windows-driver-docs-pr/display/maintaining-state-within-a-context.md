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
ms.openlocfilehash: b4a7c25efd83a59e3893358604b9fc99671fccb5
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065738"
---
# <a name="maintaining-state-within-a-context"></a>维护上下文中的状态


## <span id="ddk_maintaining_state_within_a_context_gg"></span><span id="DDK_MAINTAINING_STATE_WITHIN_A_CONTEXT_GG"></span>


在调用 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 回调时，驱动程序将更新与上下文关联的内部状态。 此回调还必须将更新的上下文的公共状态返回到 Direct3D。

 

