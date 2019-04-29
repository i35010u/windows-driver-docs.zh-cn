---
title: CM_PROB_REGISTRY_TOO_LARGE
description: CM_PROB_REGISTRY_TOO_LARGE
ms.assetid: 8870ea57-4ae4-48a0-9d56-c5d0da8e1525
keywords:
- CM_PROB_REGISTRY_TOO_LARGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9609c78fbceb0712adbc9e723e5172d6663a87bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355729"
---
# <a name="cmprobregistrytoolarge"></a>CM_PROB_REGISTRY_TOO_LARGE

此函数保留供系统使用。

注册表是太大。

## <a name="error-code"></a>错误代码

49

### <a name="display-message"></a>显示消息

"Windows 无法启动新的硬件设备，因为系统配置单元是太大 （超过了注册表大小限制）。 （代码 49）"

### <a name="recommended-resolution"></a>建议的解决方法

环境变量 DEVMGR_SHOW_NONPRESENT_DEVICES 设置为 1。 这将导致显示的已安装设备当前不存在的设备管理器。 使用设备管理器中删除这些设备。 如果注册表仍然太大，请重新安装 Windows。
