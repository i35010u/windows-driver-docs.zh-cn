---
title: CM_PROB_REGISTRY_TOO_LARGE
description: CM_PROB_REGISTRY_TOO_LARGE
keywords:
- CM_PROB_REGISTRY_TOO_LARGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d160607d0733c426bdae152c2a940b045d0d6d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827971"
---
# <a name="code-49---cm_prob_registry_too_large"></a>代码 49 - CM_PROB_REGISTRY_TOO_LARGE

此设备管理器错误消息指示注册表太大。

## <a name="error-code"></a>错误代码

49

### <a name="display-message"></a>显示消息

"Windows 无法启动新硬件设备，因为系统配置单元太大 (超出了注册表大小限制) 。  (代码 49) "

### <a name="recommended-resolution"></a>推荐的解决方案

将环境变量 DEVMGR_SHOW_NONPRESENT_DEVICES 设置为1。 这会导致设备管理器显示当前不存在的已安装设备。 使用设备管理器删除这些设备。 如果注册表仍然太大，请重新安装 Windows。
