---
title: CM_PROB_IRQ_TRANSLATION_FAILED
description: CM_PROB_IRQ_TRANSLATION_FAILED
ms.assetid: fafd40d5-43bf-4243-907a-df523e1b501e
keywords:
- CM_PROB_IRQ_TRANSLATION_FAILED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d8dc6769ed69c7b6a1b9e9d4d840ea02b0ea211
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279535"
---
# <a name="code-36---cm_prob_irq_translation_failed"></a>代码 36-CM_PROB_IRQ_TRANSLATION_FAILED

此设备管理器错误消息指示设备的 IRQ 转换失败。

## <a name="error-code"></a>错误代码

36

### <a name="display-message"></a>显示消息

"此设备正在请求 PCI 中断，但是为 ISA 中断配置（反之亦然）。 请用计算机的系统设置程序来重新配置这个设备的中断。 （代码36） "

### <a name="recommended-resolution"></a>建议的解决方法

如果有这样的选项，请尝试使用 BIOS 安装实用程序更改 IRQ 保留设置。 （BIOS 可能会提供用于为 PCI 或 ISA 设备保留某些 Irq 的选项。）
