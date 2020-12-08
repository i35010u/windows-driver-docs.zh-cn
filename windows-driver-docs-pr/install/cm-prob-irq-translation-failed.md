---
title: CM_PROB_IRQ_TRANSLATION_FAILED
description: CM_PROB_IRQ_TRANSLATION_FAILED
keywords:
- CM_PROB_IRQ_TRANSLATION_FAILED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 618e071b1727b793acd1b60b806263d07c12dce0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783119"
---
# <a name="code-36---cm_prob_irq_translation_failed"></a>代码 36 - CM_PROB_IRQ_TRANSLATION_FAILED

此设备管理器错误消息指示设备的 IRQ 转换失败。

## <a name="error-code"></a>错误代码

36

### <a name="display-message"></a>显示消息

"此设备正在请求 PCI 中断，但是为 ISA 中断配置了 (，反之亦然) 。 请用计算机的系统设置程序来重新配置这个设备的中断。  (代码 36) "

### <a name="recommended-resolution"></a>推荐的解决方案

如果有这样的选项，请尝试使用 BIOS 安装实用程序更改 IRQ 保留设置。  (BIOS 可以选择为 PCI 或 ISA 设备保留某些 Irq。 ) 
