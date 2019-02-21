---
Description: WPD Driver Development Tools
title: WPD 驱动程序开发工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ff80ca0e686f2a854b62cb71e41da25f32cea00
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525365"
---
# <a name="wpd-driver-development-tools"></a>WPD 驱动程序开发工具


Windows 便携式设备 (WPD) 提供了三个工具与 Windows 驱动程序工具包，它可用于开发 WPD 设备驱动程序。 这些工具是下表中所述。

| 工具                     | 描述                                                                                                                                                                                                                                                                                                                                                              |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *WpdDeviceInspector.exe* | 此工具用于查询 WPD 驱动程序并生成全面的 HTML 报告，其中介绍了你的设备和其功能。 例如，该工具可用于检索受支持的设备命令和对象的列表。 它还将生成所有支持的每个对象的属性的列表。                                                   |
| *WpdInfo.exe*            | 此工具执行常见的 WPD 操作，如打开和关闭设备、 创建或删除设备上的对象和发出设备的命令。 支持的属性、 命令、 内容类型、 事件和在设备级别、 服务级别，或两者的格式，还可以显示此工具。 此外，它可以为给定设备上显示每个对象的属性。 |
| *NetMon.exe*             | 此工具将记录 WPD 应用程序和 WPD 驱动程序之间的通信。                                                                                                                                                                                                                                                                                                   |

 

除了使用 Windows 驱动程序工具包提供的工具，您可能还想要安装 Windows SDK 并使用在此工具包中找到的两个 WPD 示例应用程序来浏览并测试 WPD 驱动程序。 这些示例应用程序是下表中所述。

| 应用程序                | 描述                                                                                                                                                                                    |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *WpdApiSample.exe*         | 可以使用此应用程序可以执行 WPD 设备，例如，枚举设备，列出在设备上的内容和传输内容或从设备上的常规 WPD 操作。       |
| *WpdServicesApiSample.exe* | 此应用程序可用于执行 WPD WPD 设备实现联系人设备服务上的操作。 （请注意，此应用程序仅适用于 WpdServiceSampleDriver。） |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


****
[使用 WpdInfo 工具](using-the-wpdinfo-tool.md)

[使用 WpdDeviceInspector 工具](using-the-wpddeviceinspector-tool.md)

[使用 NetMon 工具](using-the-netmon-tool.md)

 

 





