---
title: CM_PROB_NOT_CONFIGURED
description: CM_PROB_NOT_CONFIGURED
ms.assetid: 8bdc741c-6e1e-46ab-ab2d-fafe87bbd99f
keywords:
- CM_PROB_NOT_CONFIGURED
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2af9e3bbf74db543a7ed9209bff90f519f3cb564
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279514"
---
# <a name="code-1---cm_prob_not_configured"></a>代码 1-CM_PROB_NOT_CONFIGURED

此设备管理器错误消息指示系统上没有**ConfigFlags**注册表项存在设备。 这意味着未安装任何驱动程序。 通常，这意味着找不到 INF 文件。

## <a name="error-code"></a>错误代码

1

### <a name="display-message"></a>显示消息

"此设备的配置不正确。 （代码1） "

"若要更新此设备的驱动程序，请单击" 更新驱动程序 "。 如果这不起作用，请参阅硬件文档以了解详细信息。 "

### <a name="recommended-resolution"></a>建议的解决方法

选择 "**更新驱动程序**"，这将启动硬件更新向导。

## <a name="for-driver-developers"></a>面向驱动程序开发人员

此错误表示 PnP 尚未尝试安装设备。 重试安装。

如果此问题状态与[Bug 检查0x7B： INACCESSIBLE_BOOT_DEVICE](../debugger/bug-check-0x7b--inaccessible-boot-device.md)并且设备位于启动磁盘的路径上，则系统缺少启动关键设备的驱动程序。
