---
title: CM_PROB_WAITING_ON_DEPENDENCY
description: CM_PROB_WAITING_ON_DEPENDENCY
ms.assetid: 2f45c507-1926-47f4-aca8-f8b834c58601
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3a6732da2ed818cb8566423b81ff79dd15a8fd7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555217"
---
# <a name="cmprobwaitingondependency"></a>CM_PROB_WAITING_ON_DEPENDENCY

此函数保留供系统使用。

设备未启动，因为它尚未启动的另一台设备上具有依赖项。

## <a name="error-code"></a>错误代码

51

### <a name="display-message"></a>显示消息

"此设备目前正在等待另一个设备或要启动的设备组上。 （代码 51）。"

### <a name="recommended-resolution"></a>建议的解决方法

目前没有解决方法，此问题。

若要帮助诊断问题，请查看其他失败中的设备[设备树](https://msdn.microsoft.com/library/windows/hardware/ff543194)可能依赖于此设备。 如果可以确定相关的另一台设备未启动，您可能能够解决此问题。
