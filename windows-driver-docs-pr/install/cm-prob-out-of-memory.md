---
title: CM_PROB_OUT_OF_MEMORY
description: CM_PROB_OUT_OF_MEMORY
ms.assetid: 60b94407-2d06-43d9-b7e1-1ae74c28a216
keywords:
- CM_PROB_OUT_OF_MEMORY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f1f40fbbe977ab8ec325772863665211ce89e6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533032"
---
# <a name="cmproboutofmemory"></a>CM_PROB_OUT_OF_MEMORY

此函数保留供系统使用。

系统耗尽内存 − 是可能系统内存不足。

## <a name="error-code"></a>错误代码

3

### <a name="display-message"></a>显示消息

"此设备的驱动程序可能已损坏，或者您的系统的内存或其他资源不足。 （代码 3）"

### <a name="recommended-resolution"></a>建议的解决方法

如果设备驱动程序已损坏，更新的驱动程序。

若要更新的设备驱动程序，请按照下列步骤：

1. [打开设备管理器](using-device-manager.md)。

2. 右键单击表示在设备管理器窗口中的设备的图标。

3. 在显示的菜单，单击**更新驱动程序**以启动硬件更新向导。

如果设备的驱动程序运行正常，但计算机具有足够的内存设备和其他应用程序能够同时运行，无法关闭一些应用程序以释放足够的内存来运行设备。

若要检查可用内存和系统资源，请按照下列步骤：

1. 单击**启动**菜单。

2. 指向以下一系列子菜单：**所有程序**，**附件**，和**系统工具**。

3. 上**系统工具**菜单上，单击**系统信息**以确定是否足以运行设备的可用物理内存量。

您可能需要安装其他随机存取内存 (RAM) 运行某个设备。
