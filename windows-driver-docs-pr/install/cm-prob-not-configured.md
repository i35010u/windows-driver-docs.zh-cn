---
title: CM_PROB_NOT_CONFIGURED
description: CM_PROB_NOT_CONFIGURED
keywords:
- CM_PROB_NOT_CONFIGURED
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: d82b4916c7f7fb6cea4c4e3ad7c7ff37a4c229b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783087"
---
# <a name="code-1---cm_prob_not_configured"></a>代码 1 - CM_PROB_NOT_CONFIGURED

此设备管理器错误消息指示系统上没有 **ConfigFlags** 注册表项存在设备。 这意味着未安装任何驱动程序。 通常，这意味着找不到 INF 文件。

## <a name="error-code"></a>错误代码

1

### <a name="display-message"></a>显示消息

"此设备的配置不正确。  (代码 1) "

"若要更新此设备的驱动程序，请单击" 更新驱动程序 "。 如果这不起作用，请参阅硬件文档以了解详细信息。 "

### <a name="recommended-resolution"></a>推荐的解决方案

选择 " **更新驱动程序**"，这将启动硬件更新向导。

## <a name="for-driver-developers"></a>面向驱动程序开发人员

此错误表示 PnP 尚未尝试安装设备。 重试安装。

如果此问题状态与 [Bug 检查0x7B： INACCESSIBLE_BOOT_DEVICE](../debugger/bug-check-0x7b--inaccessible-boot-device.md) 并且设备位于启动磁盘的路径上，则系统缺少启动关键设备的驱动程序。
