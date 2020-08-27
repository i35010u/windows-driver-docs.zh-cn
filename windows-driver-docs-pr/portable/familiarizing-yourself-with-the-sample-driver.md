---
description: WPD 驱动程序开发工具
title: WPD 驱动程序开发工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ad74219e65b03c675ca689181bc4ab810309a37
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968512"
---
# <a name="wpd-driver-development-tools"></a>WPD 驱动程序开发工具


Windows 便携式设备 (WPD) 提供三个使用 Windows 驱动程序工具包的工具，可用于开发 WPD 设备驱动程序。 下表描述了这些工具。

| 工具                     | 说明                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *WpdDeviceInspector.exe* | 此工具旨在查询 WPD 驱动程序，并生成全面的 HTML 报告，用于描述设备及其功能。 例如，可以使用工具检索受支持的设备命令和对象的列表。 它还将生成每个对象支持的所有属性的列表。                                                   |
| *WpdInfo.exe*            | 此工具执行常见的 WPD 操作，例如打开和关闭设备、在设备上创建或删除对象以及发出设备命令。 此工具还可以在设备级别和/或服务级别显示支持的属性、命令、内容类型、事件和格式。 此外，它还可以显示给定设备上每个对象的属性。 |
| *NetMon.exe*             | 此工具记录 WPD 应用程序与 WPD 驱动程序之间的流量。                                                                                                                                                                                                                                                                                                   |

 

除了 Windows 驱动程序工具包附带的工具外，您可能还需要安装 Windows SDK，并使用此工具包中的两个 WPD 示例应用程序来浏览和测试 WPD 驱动程序。 下表介绍了这些示例应用程序。

| 应用程序                | 说明                                                                                                                                                                                    |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *WpdApiSample.exe*         | 你可以使用此应用程序在 WPD 设备上执行常见的 WPD 操作，例如枚举设备、列出设备上的内容，以及将内容传输到设备或从设备传输内容。       |
| *WpdServicesApiSample.exe* | 可以使用此应用程序在实现联系人设备服务的 WPD 设备上执行 WPD 操作。  (请注意，此应用程序仅适用于 WpdServiceSampleDriver。 )  |

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[使用 WpdInfo 工具](using-the-wpdinfo-tool.md)

[使用 WpdDeviceInspector 工具](using-the-wpddeviceinspector-tool.md)

[使用 NetMon 工具](using-the-netmon-tool.md)

 

 





