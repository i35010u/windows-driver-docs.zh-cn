---
title: CM_PROB_REGISTRY_TOO_LARGE
description: CM_PROB_REGISTRY_TOO_LARGE
ms.assetid: 8870ea57-4ae4-48a0-9d56-c5d0da8e1525
keywords:
- CM_PROB_REGISTRY_TOO_LARGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40ce2223c8144f0b8439bfefba4c04e7c8c1a4a4
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279494"
---
# <a name="code-49---cm_prob_registry_too_large"></a>代码 49-CM_PROB_REGISTRY_TOO_LARGE

此设备管理器错误消息指示注册表太大。

## <a name="error-code"></a>错误代码

49

### <a name="display-message"></a>显示消息

"Windows 无法启动新硬件设备，因为系统配置单元太大（超过了注册表大小限制）。 （代码49） "

### <a name="recommended-resolution"></a>建议的解决方法

将环境变量 DEVMGR_SHOW_NONPRESENT_DEVICES 设置为1。 这会导致设备管理器显示当前不存在的已安装设备。 使用设备管理器删除这些设备。 如果注册表仍然太大，请重新安装 Windows。
