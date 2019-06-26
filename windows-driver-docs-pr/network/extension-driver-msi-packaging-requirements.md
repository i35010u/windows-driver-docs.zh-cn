---
title: 扩展驱动程序 MSI 打包要求
description: 交换机扩展必须打包到可以无提示方式安装的 MSI 文件中。
ms.assetid: 300118F9-D9C7-4AFA-B54A-59666BC680F1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79b2a513ad0e1590a3175f45f23213ea10497d06
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353746"
---
# <a name="extension-driver-msi-packaging-requirements"></a>扩展驱动程序 MSI 打包要求


交换机扩展必须打包到可以无提示方式安装的 MSI 文件中。 然后，此文件都可以部署到其中扩展管理应用程序自动使用的计算机。

MSI 文件必须满足以下要求：

-   驱动程序必须打包并分发的标准的 MSI 包格式。
-   必须以无提示方式卸载 MSI 包。
-   MSI 包可以包含只有一个扩展。
-   MSI 包必须包含所需的表下面列出的 MSI 表字段中所述的字段。 此外，MSI 文件必须能够以无提示方式安装驱动程序.sys、.inf 和所需的驱动程序使用的参数中所述运行任何补充文件*DriverInstallParams* MSI 属性表的字段下面的字段列表。

| 字段                           | 必需 | 在任务栏的搜索框中键入       | 详细信息                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|---------------------------------|----------|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **说明**                 | 必需 | **String** | 扩展显示的的说明。                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| **Manufacturer**                | 必需 | **String** | 发布扩展驱动程序的公司名称。 可以存储已本地化的字符串。                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **ProductVersion**              | 必需 | **String** | 此版本的 MSI 包。 例如：1.0.0.0                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **ProductName**                 | 必需 | **String** | 驱动程序的名称。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| **DriverID**                    | 必需 | **String** | 必须匹配 Msvm\_InstalledEthernetSwitchExtension.Name 可用字段，则后安装该驱动程序和驱动程序的 INF 文件中的驱动程序 ID。                                                                                                                                                                                                                                                                                                                                                    |
| **DriverVersion**               | 必需 | **String** | 此程序包中包含的驱动程序版本。 例如：1.0.0.0                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| **ExtensionType**               | 必需 | **String** | 扩展的类型。 值：转发，捕获、 监视、 筛选器                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| **DriverInstallParams**         | 必需 | **String** | 若要以无提示方式安装此驱动程序所使用的参数。 示例： /q                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| **IsManagedByExtensionManager** | 可选 | **String** | 存在且非零值 = 是，0 或不存在 = 否                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| **MinApplicableOSVersion**      | 必需 | **String** | 此扩展将在上运行的 Windows 操作系统最低版本。 操作系统版本号，请参阅操作系统版本。 请注意，HYPER-V 可扩展交换机功能已添加在 Windows Server 2012 中，因此此字段的最低有效值为"6.2"。                                                                                                                                                                                                                    |
| **MaxApplicableOSVersion**      | 可选 | **String** | 此扩展将在上运行的 Windows 操作系统最大版本。 请参阅[Operating System Version](https://docs.microsoft.com/windows/desktop/SysInfo/operating-system-version)对于操作系统的版本号。 请注意，HYPER-V 可扩展交换机功能已添加在 Windows Server 2012 中，因此此字段的最低有效值是"6.2"或的值**MinApplicableOSVersion**，大者为准。 此字段是可选字段。 如果未不指定任何值，此扩展将运行**MinApplicableOSVersion**及更高版本。 |

 

 

 





