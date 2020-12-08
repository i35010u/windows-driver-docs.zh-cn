---
title: CM_PROB_DISABLED_SERVICE
description: CM_PROB_DISABLED_SERVICE
keywords:
- CM_PROB_DISABLED_SERVICE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a88d0d3c0460022f82b53942731a1b5f45c7ced1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806281"
---
# <a name="code-32---cm_prob_disabled_service"></a>代码 32 - CM_PROB_DISABLED_SERVICE

此设备管理器错误消息指示驱动程序已被禁用。

## <a name="error-code"></a>错误代码

32

### <a name="display-message"></a>显示消息

"此设备 (服务) 的驱动程序已被禁用。 另一个驱动程序可以提供这个功能。  (代码 32) "

### <a name="recommended-resolution"></a>推荐的解决方案

在注册表中，此服务的启动类型设置为 "已禁用"。 如果该驱动程序是必需的，则更改启动类型。
