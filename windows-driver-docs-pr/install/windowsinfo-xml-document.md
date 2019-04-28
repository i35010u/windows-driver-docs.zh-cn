---
title: WindowsInfo XML 文档
description: WindowsInfo XML 文档
ms.assetid: 8004d165-46c5-4bf4-849d-ba83205b9f54
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82ebc8266c4e0cb16f0c735cda6dea0ebfab2506
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339256"
---
# <a name="windowsinfo-xml-document"></a>WindowsInfo XML 文档


本文档包含用于指定显示执行的操作，操作系统的设备元数据包中指定的设备数据。 这些操作包括以下各项：

-   是否[设备图标](device-icon-file.md)当设备进入断开连接状态，例如当用户删除设备时显示。 此操作指定的[ **ShowDeviceInDisconnectedState** ](https://msdn.microsoft.com/library/windows/hardware/ff552242) WindowsInfo XML 文档内的 XML 元素。

-   是否 Device Stage 用户界面出现当设备从断开连接的状态转换到已连接的状态，例如当用户插入设备中。 此操作指定的[ **LaunchDeviceStageOnDeviceConnect** ](https://msdn.microsoft.com/library/windows/hardware/ff548633) WindowsInfo XML 文档内的 XML 元素。

-   当用户双击是否启动 Device Stage 用户界面[设备图标](device-icon-file.md)任一设备和打印机用户界面中或在 Windows 资源管理器中显示。 此操作指定的[ **LaunchDeviceStageFromExplorer** ](https://msdn.microsoft.com/library/windows/hardware/ff548629) WindowsInfo XML 文档内的 XML 元素。

每个设备元数据包必须包含一个 WindowsInfo XML 文档。 文档的名称必须是*WindowsInfo.xml*。

WindowsInfo XML 文档中的数据会基于设置格式[WindowsInfo XML 架构](https://msdn.microsoft.com/library/windows/hardware/ff553992)。

 

 





