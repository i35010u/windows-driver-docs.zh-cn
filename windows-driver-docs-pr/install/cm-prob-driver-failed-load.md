---
title: CM_PROB_DRIVER_FAILED_LOAD
description: CM_PROB_DRIVER_FAILED_LOAD
ms.assetid: 84d88db9-338b-4318-ba05-696521c96dd6
keywords:
- CM_PROB_DRIVER_FAILED_LOAD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8565d102528ec239f7034fc4133d887aaf51cf1c
ms.sourcegitcommit: 8739f3683432345092305565815baa68c82bef43
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "96482565"
---
# <a name="code-39---cm_prob_driver_failed_load"></a>代码 39 - CM_PROB_DRIVER_FAILED_LOAD

此设备管理器错误消息指示无法加载驱动程序。

## <a name="error-code"></a>错误代码

39

### <a name="display-message"></a>显示消息

"Windows 无法加载此硬件的设备驱动程序。 驱动程序可能已损坏或丢失。  (代码 39) "

### <a name="recommended-resolution"></a>推荐的解决方案

重新安装或获取新驱动程序。

此错误的一些常见原因包括：

- 某个驱动程序文件不存在、一个已损坏的二进制文件、一个文件 i/o 问题或引用另一个二进制文件中的入口点的驱动程序无法加载。

- 系统启用了 [虚拟机监控程序保护的代码完整性](https://docs.microsoft.com/windows-hardware/test/hlk/testref/driver-compatibility-with-device-guard) ，驱动程序与该功能不兼容。

