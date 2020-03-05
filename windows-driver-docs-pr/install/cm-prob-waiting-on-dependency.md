---
title: CM_PROB_WAITING_ON_DEPENDENCY
description: CM_PROB_WAITING_ON_DEPENDENCY
ms.assetid: 2f45c507-1926-47f4-aca8-f8b834c58601
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d7cc2065e74f7c1521e40e098f7e53a69879537
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279464"
---
# <a name="code-51---cm_prob_waiting_on_dependency"></a>代码 51-CM_PROB_WAITING_ON_DEPENDENCY

此设备管理器错误消息表明设备没有启动，因为它与另一台尚未启动的设备有依赖关系。

## <a name="error-code"></a>错误代码

51

### <a name="display-message"></a>显示消息

"此设备目前正在等待另一个设备或一组设备启动。 （代码51）。 "

### <a name="recommended-resolution"></a>建议的解决方法

目前不能解决此问题。

若要帮助诊断此问题，请检查[设备树](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)中此设备可能依赖的其他故障设备。 如果可以确定另一个相关设备无法启动的原因，您可能能够解决此问题。
