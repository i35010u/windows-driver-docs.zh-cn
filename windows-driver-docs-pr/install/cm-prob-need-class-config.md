---
title: CM_PROB_NEED_CLASS_CONFIG
description: CM_PROB_NEED_CLASS_CONFIG
ms.assetid: e9604fcb-61c2-4b94-af53-c9278bc05dd0
keywords:
- CM_PROB_NEED_CLASS_CONFIG
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 28860c16bee71e2045790b780d2511060cbb63a0
ms.sourcegitcommit: f63852446e614c985a65f599cdfe788bdb0c6089
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2020
ms.locfileid: "87425736"
---
# <a name="code-56---cm_prob_need_class_config"></a>代码 56 - CM_PROB_NEED_CLASS_CONFIG

此设备管理器错误消息表明 Windows 仍在为此设备设置类配置。


## <a name="error-code"></a>错误代码

56

### <a name="display-message"></a>显示消息

"Windows 仍在为此设备设置类配置。 （代码56） "


## <a name="for-driver-developers"></a>面向驱动程序开发人员

此问题代码通常是暂时性的。

对于某些设备安装程序类，在使用驱动程序包安装设备后，需要进行其他类配置操作才能使设备正常运行。  配置完成后，将重新启动设备，并且不再应有此问题代码。

例如，网络类设备根据 `*IfType` 、 `UpperRange` 和其他特定于网络的 INF 指令接收其他配置。

如果某个网络类设备继续具有此问题代码，则驱动程序 INF 可能具有无效的网络特定 INF 指令，或者系统的网络状态可能已损坏，需要重置。

为此，请使用 "设置" 应用中的 "网络重置" 按钮。
