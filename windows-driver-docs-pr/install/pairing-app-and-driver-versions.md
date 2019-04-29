---
title: 将驱动程序与通用 Windows 平台 (UWP) 应用配对
description: 本主题介绍如何指定特定驱动程序是否存在应仅加载通用 Windows 平台 (UWP) 应用。
ms.assetid: 50f981bb-e17b-4454-88f9-46b09eb05509
ms.date: 08/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f31245dd44ee9597907614accdb956592fa84b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363344"
---
# <a name="pairing-a-driver-with-a-universal-windows-platform-uwp-app"></a>将驱动程序与通用 Windows 平台 (UWP) 应用配对

从 Windows 10 1709年版开始，可以指定特定驱动程序是否存在应仅加载通用 Windows 平台 (UWP) 应用。 使用此选项时，Microsoft Store 提供每个用户最新版本的适用于已安装版本的驱动程序，该用户的计算机的应用。

应用程序还可以进一步约束加载到特定的驱动程序版本或日期。  本主题介绍应用程序和驱动程序中创建此类需求所需的步骤。

## <a name="steps-in-the-app"></a>在应用中的步骤

若要使 UWP 应用将仅当存在特定的驱动程序时，将两个 XML 元素添加到应用程序的清单 XML (.appx) 文件中：

* [uap5:DriverDependency](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverdependency)
* [uap5:DriverConstraint](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverconstraint)

具体而言，使用这些元素指定至少一个包含至少一个驱动程序约束的驱动程序依赖关系。  有关使用这些元素链接到更高版本的参考页上，请参阅更多详细信息。  后一种页面包含一个示例。

## <a name="steps-in-the-driver"></a>驱动程序中的步骤

接下来，执行以下操作，驱动程序的 INF 文件中：

1. 指定[INF AddSoftware 指令](inf-addsoftware-directive.md)。
2. 设置**SoftwareType**为 2 的条目。
3. 提供包系列名称 (PFN) 中**SoftwareID**条目。

除了匹配的最新的应用程序和驱动程序版本，系统还会尝试匹配上一个应用程序和驱动程序版本。  例如，如果应用程序版本 2 指定最小的驱动程序版本 2，而应用程序版本 1 指定最小的驱动程序版本 1，驱动程序版本 1 的系统已成功将加载应用程序版本 1。

## <a name="see-also"></a>请参阅

* [uap5:DriverDependency](https://docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverdependency)
* [uap5:DriverConstraint](https://review.docs.microsoft.com/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverconstraint?branch=lahugh-rs3)
* [INF AddSoftware 指令](inf-addsoftware-directive.md)
* [硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)
* [硬件支持应用 (HSA)：适用于应用开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-app-developers.md)
