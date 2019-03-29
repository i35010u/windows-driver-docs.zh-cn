---
title: CM_PROB_DRIVER_BLOCKED
description: CM_PROB_DRIVER_BLOCKED
ms.assetid: dfe5f8f9-8430-4f80-9b1c-179f699617f8
keywords:
- CM_PROB_DRIVER_BLOCKED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdd3fc2822b6de7768d47b50847470071315a6d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564972"
---
# <a name="cmprobdriverblocked"></a>CM_PROB_DRIVER_BLOCKED

此函数保留供系统使用。

系统不会加载该驱动程序，因为它会列入[Windows 驱动程序保护](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)数据库提供[Windows Update](https://msdn.microsoft.com/windows-drivers/develop/distributing_a_driver_package_win8)*。*

## <a name="error-code"></a>错误代码

48

### <a name="display-message"></a>显示消息

"此设备的软件已被阻止的启动，因为它可被识别有问题 Windows。 新的驱动程序，请与硬件供应商联系。 （代码 48）"

### <a name="recommended-resolution"></a>建议的解决方法

从硬件供应商处获取新的驱动程序。
