---
title: 将驱动程序与通用 Windows 平台 (UWP) 应用配对
description: 本主题介绍如何指定通用 Windows 平台 (UWP) 应用程序只应在存在特定驱动程序时加载。
ms.assetid: 50f981bb-e17b-4454-88f9-46b09eb05509
ms.date: 08/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 028112a5eef9d32e392b47decefedf6ad4596e3d
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095809"
---
# <a name="pairing-a-driver-with-a-universal-windows-platform-uwp-app"></a>将驱动程序与通用 Windows 平台 (UWP) 应用配对

从 Windows 10 版本1709开始，你可以指定通用 Windows 平台 (UWP) 应用程序只应在存在特定驱动程序时加载。 使用此选项时，Microsoft Store 向每个用户提供应用程序的最新版本，该应用程序适用于该用户计算机上安装的驱动程序版本。

应用可以进一步限制加载到特定驱动程序版本或日期。  本主题介绍了在应用程序 **和驱动程序** 中创建此类要求所需的步骤。

> [!NOTE]
> 应用程序 *和* 驱动程序 *必须* 声明对应用程序 (HSA) 的依赖关系。  

## <a name="steps-in-the-app"></a>应用中的步骤

若要使 UWP 应用仅在特定驱动程序存在时加载，请将两个 XML 元素添加到应用的清单 XML ( .appx) 文件中：

* [uap5:DriverDependency](/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverdependency)
* [uap5:DriverConstraint](/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverconstraint)

具体而言，请使用这些元素来指定至少一个包含至少一个驱动程序约束的驱动程序依赖项。  有关使用这些元素的详细信息，请参阅链接到上述的参考页。  后一页包含一个示例。

## <a name="steps-in-the-driver"></a>驱动程序中的步骤

接下来，请在驱动程序的 INF 文件中执行以下操作：

1. 指定 [INF AddSoftware 指令](inf-addsoftware-directive.md)。
2. 将 **SoftwareType** 项设置为2。
3. 在 **SoftwareID** 条目中提供包系列名称 (PFN) 。

除了匹配最新的应用程序和驱动程序版本以外，系统还会尝试匹配以前的应用程序版本和驱动程序版本。  例如，如果应用版本2指定最低驱动程序版本2，而应用版本1指定最低驱动程序版本1，则具有驱动程序版本1的系统将成功加载应用版本1。

## <a name="see-also"></a>另请参阅

* [uap5:DriverDependency](/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverdependency)
* [uap5:DriverConstraint](/uwp/schemas/appxpackage/uapmanifestschema/element-uap5-driverconstraint)
* [INF AddSoftware 指令](inf-addsoftware-directive.md)
* [硬件支持应用 (HSA) ：驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)
* [硬件支持应用 (HSA) ：适用于应用开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-app-developers.md)