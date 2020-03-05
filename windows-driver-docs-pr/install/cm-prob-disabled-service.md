---
title: CM_PROB_DISABLED_SERVICE
description: CM_PROB_DISABLED_SERVICE
ms.assetid: b2447b01-c25d-4761-bc96-291d508feb15
keywords:
- CM_PROB_DISABLED_SERVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3a70b04d22b31a3d9fc7798b2fc4f17589101b1
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279588"
---
# <a name="code-32---cm_prob_disabled_service"></a>代码 32-CM_PROB_DISABLED_SERVICE

此设备管理器错误消息指示驱动程序已被禁用。

## <a name="error-code"></a>错误代码

32

### <a name="display-message"></a>显示消息

"此设备的驱动程序（服务）已禁用。 另一个驱动程序可以提供这个功能。 （代码32） "

### <a name="recommended-resolution"></a>建议的解决方法

在注册表中，此服务的启动类型设置为 "已禁用"。 如果该驱动程序是必需的，则更改启动类型。
