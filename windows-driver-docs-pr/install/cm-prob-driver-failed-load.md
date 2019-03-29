---
title: CM_PROB_DRIVER_FAILED_LOAD
description: CM_PROB_DRIVER_FAILED_LOAD
ms.assetid: 84d88db9-338b-4318-ba05-696521c96dd6
keywords:
- CM_PROB_DRIVER_FAILED_LOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4475a6a03a90d34ed1a8af2fe862f42021bfebb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567616"
---
# <a name="cmprobdriverfailedload"></a>CM_PROB_DRIVER_FAILED_LOAD

此函数保留供系统使用。

无法加载该驱动程序。

## <a name="error-code"></a>错误代码

39

### <a name="display-message"></a>显示消息

"Windows 无法加载这个硬件设备驱动程序。 该驱动程序可能已损坏或丢失。 （代码 39）"

### <a name="recommended-resolution"></a>建议的解决方法

重新安装或获取新的驱动程序。

此错误的原因包括：

- 不存在的驱动程序文件、 已损坏的二进制文件、 文件 I/O 问题或引用中无法加载的另一个二进制文件的入口点的驱动程序。

- 该驱动程序不符合[内核模式代码签署策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。
