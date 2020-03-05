---
title: CM_PROB_CONSOLE_LOCKED
description: CM_PROB_CONSOLE_LOCKED
ms.assetid: b2086640-0103-41ee-8d60-db1126e482de
keywords:
- CM_PROB_CONSOLE_LOCKED
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4a22769150b9e1ab5b702135b5b5813595afaa9b
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279970"
---
# <a name="code-55---cm_prob_console_locked"></a>代码 55-CM_PROB_CONSOLE_LOCKED

此设备管理器错误消息指示由于组策略/MDM （Intune）策略可防止 DMA 攻击，导致设备被阻止。




## <a name="error-code"></a>错误代码

55

### <a name="display-message"></a>显示消息

"此设备在用户未登录时被阻止启动。 （代码55） "


### <a name="recommended-resolution"></a>建议的解决方法

有关内核 DMA 保护的详细信息，请参阅 https://docs.microsoft.com/windows/security/information-protection/kernel-dma-protection-for-thunderbolt。

