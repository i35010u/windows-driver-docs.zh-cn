---
title: CM_PROB_DRIVER_FAILED_LOAD
description: CM_PROB_DRIVER_FAILED_LOAD
ms.assetid: 84d88db9-338b-4318-ba05-696521c96dd6
keywords:
- CM_PROB_DRIVER_FAILED_LOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef92d58401433ea83bf25600dd2cbb15e20156f1
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558413"
---
# <a name="cm_prob_driver_failed_load"></a>CM_PROB_DRIVER_FAILED_LOAD

此函数保留供系统使用。

无法加载该驱动程序。

## <a name="error-code"></a>错误代码

39

### <a name="display-message"></a>显示消息

"Windows 无法加载此硬件的设备驱动程序。 驱动程序可能已损坏或丢失。 （代码39） "

### <a name="recommended-resolution"></a>建议的解决方法

重新安装或获取新驱动程序。

此错误的原因包括：

- 某个驱动程序文件不存在、一个已损坏的二进制文件、一个文件 i/o 问题或引用另一个二进制文件中的入口点的驱动程序无法加载。

- 该驱动程序不符合[内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。

