---
title: CM_PROB_REGISTRY
description: CM_PROB_REGISTRY
keywords:
- CM_PROB_REGISTRY
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca27df00bd712cd4850f8979bfac08b635a6b45c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783077"
---
# <a name="code-19---cm_prob_registry"></a>代码 19 - CM_PROB_REGISTRY

此设备管理器错误消息指示检测到注册表问题。

## <a name="error-code"></a>错误代码

19

### <a name="display-message"></a>显示消息

"Windows 无法启动此硬件设备，因为其在注册表) 中 (的配置信息不完整或已损坏。  (代码 19) "

### <a name="recommended-resolution"></a>推荐的解决方案

如果为设备定义了多个服务，打开服务密钥时出现故障，或者无法从服务密钥获取驱动程序名称，则会导致此错误。

尝试卸载然后重新安装驱动程序，或将系统回滚到最新的注册表配置。

若要卸载并重新安装设备驱动程序，请执行以下步骤：

1. [打开设备管理器](using-device-manager.md)。

2. 右键单击 "设备管理器" 窗口中代表该设备的图标。

3. 在出现的菜单中，单击 " **卸载** " 以卸载设备驱动程序。

4. 在设备管理器菜单栏上单击 " **操作** "。

5. 在 " **操作** " 菜单上，单击 " **扫描检测硬件改动** " 以重新安装设备驱动程序。

若要将系统回滚到最新的注册表配置，请在安全模式下重新启动计算机，然后选择 "最后一次正确的配置" 选项。
