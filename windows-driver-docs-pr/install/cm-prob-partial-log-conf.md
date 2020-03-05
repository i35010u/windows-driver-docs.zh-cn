---
title: CM_PROB_PARTIAL_LOG_CONF
description: CM_PROB_PARTIAL_LOG_CONF
ms.assetid: 1e8b10e8-c2c6-4a71-9af5-575206098148
keywords:
- CM_PROB_PARTIAL_LOG_CONF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a78ae518332b258b2ca143bd29ab9e56e0ff4fd2
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279504"
---
# <a name="code-16---cm_prob_partial_log_conf"></a>代码 16-CM_PROB_PARTIAL_LOG_CONF

此设备管理器错误消息指示设备只能部分配置。

## <a name="error-code"></a>错误代码

16

### <a name="display-message"></a>显示消息

"Windows 无法识别该设备使用的所有资源。 （代码16） "

"若要指定此设备的其他资源，请单击" 资源 "选项卡，并填写缺少的设置。 请检查硬件文档，找出要使用的设置。

### <a name="recommended-resolution"></a>建议的解决方法

手动配置设备所需的资源。

若要配置设备资源，请执行以下步骤：

1. [打开设备管理器](using-device-manager.md)。

2. 双击 "设备管理器" 窗口中表示该设备的图标。

3. 在出现的 "设备属性" 页上，单击 "**资源**" 选项卡。设备资源列在 "**资源**" 页上的 "**资源设置**" 列表中。

4. 如果 "**资源设置**" 列表中的某个资源旁有一个问号，请选择该资源将其分配给设备。

5. 如果资源无法更改，请单击 "**更改设置**"。 如果 "**更改设置**" 不可用，请尝试清除 "**使用自动设置**" 复选框以使其可用。

如果设备不是即插即用设备，请在设备文档中查看有关如何为设备配置资源的详细信息。
