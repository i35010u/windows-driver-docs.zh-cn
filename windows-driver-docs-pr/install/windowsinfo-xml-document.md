---
title: WindowsInfo XML 文档
description: WindowsInfo XML 文档
ms.assetid: 8004d165-46c5-4bf4-849d-ba83205b9f54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c3ae032a7ea8d83f491bb7c5cdfd277f43cde18
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097075"
---
# <a name="windowsinfo-xml-document"></a>WindowsInfo XML 文档


此文档包含的数据指定操作系统对设备元数据包中的指定设备执行的显示操作。 这些操作包括下列各项：

-   当设备处于断开连接状态时（例如，当用户删除设备时）是否显示 [设备图标](device-icon-file.md) 。 此操作由 WindowsInfo XML 文档中的 [**ShowDeviceInDisconnectedState**](/previous-versions/windows/hardware/metadata/ff552242(v=vs.85)) XML 元素指定。

-   当设备从断开连接状态过渡到已连接状态时（例如，当用户插入设备时）是否显示设备暂存用户界面。 此操作由 WindowsInfo XML 文档中的 [**LaunchDeviceStageOnDeviceConnect**](/previous-versions/windows/hardware/metadata/ff548633(v=vs.85)) XML 元素指定。

-   当用户双击出现在 "设备和打印机" 用户界面或 Windows 资源管理器中的 [设备图标](device-icon-file.md) 时，是否启动设备暂存用户界面。 此操作由 WindowsInfo XML 文档中的 [**LaunchDeviceStageFromExplorer**](/previous-versions/windows/hardware/metadata/ff548629(v=vs.85)) XML 元素指定。

每个设备元数据包必须只包含一个 WindowsInfo XML 文档。 文档的名称必须 *WindowsInfo.xml*。

WindowsInfo XML 文档中的数据基于 [WINDOWSINFO Xml 架构](/previous-versions/windows/hardware/metadata/ff553992(v=vs.85))进行格式设置。

 

