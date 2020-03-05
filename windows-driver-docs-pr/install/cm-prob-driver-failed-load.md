---
title: CM_PROB_DRIVER_FAILED_LOAD
description: CM_PROB_DRIVER_FAILED_LOAD
ms.assetid: 84d88db9-338b-4318-ba05-696521c96dd6
keywords:
- CM_PROB_DRIVER_FAILED_LOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07297f6ce47c7f3580420bf7cd2bdc7c749cf8f2
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279582"
---
# <a name="code-39---cm_prob_driver_failed_load"></a>代码 39-CM_PROB_DRIVER_FAILED_LOAD

此设备管理器错误消息指示无法加载驱动程序。

## <a name="error-code"></a>错误代码

39

### <a name="display-message"></a>显示消息

"Windows 无法加载此硬件的设备驱动程序。 驱动程序可能已损坏或丢失。 （代码39） "

### <a name="recommended-resolution"></a>建议的解决方法

重新安装或获取新驱动程序。

此错误的原因包括：

- 某个驱动程序文件不存在、一个已损坏的二进制文件、一个文件 i/o 问题或引用另一个二进制文件中的入口点的驱动程序无法加载。

- 该驱动程序不符合[内核模式代码签名策略](kernel-mode-code-signing-policy--windows-vista-and-later-.md)。

