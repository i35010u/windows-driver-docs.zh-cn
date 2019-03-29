---
title: CM_PROB_IRQ_TRANSLATION_FAILED
description: CM_PROB_IRQ_TRANSLATION_FAILED
ms.assetid: fafd40d5-43bf-4243-907a-df523e1b501e
keywords:
- CM_PROB_IRQ_TRANSLATION_FAILED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0900e559e0fd8ad4172befb8fabb0fecf54c668
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564974"
---
# <a name="cmprobirqtranslationfailed"></a>CM_PROB_IRQ_TRANSLATION_FAILED

此函数保留供系统使用。

IRQ 转换失败的设备。

## <a name="error-code"></a>错误代码

36

### <a name="display-message"></a>显示消息

"此设备正在请求 PCI 中断，但配置为 ISA 中断 （反之亦然）。 请使用计算机的系统安装程序重新配置此设备的中断。 （代码 36）"

### <a name="recommended-resolution"></a>建议的解决方法

请尝试使用 bios 设置更改设置的 IRQ 保留项，如果存在这种选项。 （在 BIOS 可能有选项保留为 PCI 或 ISA 设备特定的 Irq。）
