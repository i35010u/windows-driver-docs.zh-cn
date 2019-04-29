---
title: CM_PROB_PARTIAL_LOG_CONF
description: CM_PROB_PARTIAL_LOG_CONF
ms.assetid: 1e8b10e8-c2c6-4a71-9af5-575206098148
keywords:
- CM_PROB_PARTIAL_LOG_CONF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94d46655e164f54f415e4ee3fa87b3ac6ba03065
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360025"
---
# <a name="cmprobpartiallogconf"></a>CM_PROB_PARTIAL_LOG_CONF

此函数保留供系统使用。

该设备仅部分配置。

## <a name="error-code"></a>错误代码

16

### <a name="display-message"></a>显示消息

"Windows 无法识别此设备使用的所有资源。 （代码 16）"

"若要指定此设备的其他资源，单击资源选项卡，填写缺少的设置。 检查硬件文档，以找出要使用哪些设置。"

### <a name="recommended-resolution"></a>建议的解决方法

手动配置设备需要的资源。

若要配置设备资源，请按照下列步骤：

1. [打开设备管理器](using-device-manager.md)。

2. 双击表示设备管理器窗口中的设备的图标。

3. 在设备属性表中显示，单击**资源**选项卡。中列出了设备资源**资源设置**上列出**资源**页。

4. 如果中的资源**资源设置**列表具有它旁边的问号，选择该资源并将其分配给设备。

5. 如果某个资源不能更改，请单击**更改设置**。 如果**更改设置**不可用，请尝试清除**使用自动设置**复选框以使其可用。

如果设备不是插设备，查看设备文档了解有关如何配置设备的资源的详细信息。
