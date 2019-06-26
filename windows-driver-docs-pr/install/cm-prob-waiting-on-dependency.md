---
title: CM_PROB_WAITING_ON_DEPENDENCY
description: CM_PROB_WAITING_ON_DEPENDENCY
ms.assetid: 2f45c507-1926-47f4-aca8-f8b834c58601
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c500f222e940296e6f78fb0f7fd84877421caf78
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375342"
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

若要帮助诊断问题，请查看其他失败中的设备[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)可能依赖于此设备。 如果可以确定相关的另一台设备未启动，您可能能够解决此问题。
