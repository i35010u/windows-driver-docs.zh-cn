---
title: CM_PROB_REGISTRY
description: CM_PROB_REGISTRY
ms.assetid: 162586c4-f67f-40e8-bbbb-2b5c574732f4
keywords:
- CM_PROB_REGISTRY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 137aa07742d31511d872312a7d4b2f78f5e31194
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355749"
---
# <a name="cmprobregistry"></a>CM_PROB_REGISTRY

此函数保留供系统使用。

检测到注册表问题。

## <a name="error-code"></a>错误代码

19

### <a name="display-message"></a>显示消息

"Windows 无法启动这个硬件设备由于其配置信息 （注册表） 中的不完整或已损坏。 （代码 19）"

### <a name="recommended-resolution"></a>建议的解决方法

如果多个设备定义一个服务，会显示无法打开服务密钥，或驱动程序名称不能从此服务密钥会导致此错误。

尝试任一卸载和重新安装该驱动程序或系统回滚到注册表的最新成功配置。

若要卸载并重新安装设备驱动程序，请按照下列步骤：

1. [打开设备管理器](using-device-manager.md)。

2. 右键单击表示在设备管理器窗口中的设备的图标。

3. 在显示的菜单，单击**卸载**卸载设备驱动程序。

4. 单击**操作**设备管理器菜单栏上。

5. 上**操作**菜单上，单击**扫描检测硬件改动**重新安装设备驱动程序。

若要将系统还原到最新的成功配置的注册表，在安全模式下重新启动计算机，然后选择最后一个已知的正确配置选项。
