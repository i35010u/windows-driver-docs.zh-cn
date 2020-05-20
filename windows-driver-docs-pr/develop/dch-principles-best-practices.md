---
ms.assetid: 5865ded8-5b50-4646-a993-613b91d360fb
title: DCH 设计原则和最佳做法
description: 介绍了 Windows 驱动程序的 DCH 原则。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: d2c96949ba71ad4a77d036fc98989a150b6c5117
ms.sourcegitcommit: 958a5ced83856df22627c06eb42c9524dd547906
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83270466"
---
# <a name="dch-design-principles-and-best-practices"></a>DCH 设计原则和最佳做法

本页介绍了 Windows 驱动程序的设计原则和最佳做法。

## <a name="dch-design-principles"></a>DCH 设计原则

为了让 Windows 驱动程序符合 DCH，需要考虑三个设计原则：

- 声明性 **(D)** ：仅使用声明性 INF 指令安装驱动程序。 请勿包括共同安装程序或 RegisterDll 函数。

- 组件化 **(C)** ：特定于版本的、特定于 OEM 和可选的驱动程序自定义项独立于基础驱动程序包。 因此，可以独立于自定义项为仅提供核心设备功能的基础驱动程序设定目标、进行外部测试和提供服务。

- 硬件支持应用 **(H)** ：任何与 Windows 驱动程序关联的用户界面 (UI) 组件都必须打包为硬件支持应用 (HSA) 或预安装在 OEM 设备上。 HSA 是与驱动程序配对的可选设备特定应用。 此类应用可以是[通用 Windows 平台 (UWP)](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide)，也可以是[桌面桥应用](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root)。 必须通过 Microsoft Store 分发和更新 HSA。 有关详细信息，请参阅[硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-support-app--hsa--steps-for-driver-developers)和[硬件支持应用 (HSA)：适用于应用开发人员的步骤](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-support-app--hsa--steps-for-app-developers)。

首字母缩略词“DCH”指的是上面列出的原则。 请参阅[符合 DCH 的驱动程序包示例](dch-example.md)页，以了解驱动程序示例如何应用 DCH 设计原则。

## <a name="overview"></a>概述 

符合 DCH 的驱动程序包中有 INF 文件，以及在[基于通用 Windows 平台 (UWP) 的 Windows 10 版本](target-platforms.md)上安装和运行的二进制文件。 它们还在共用一组公用接口的其他 Windows 10 版本上安装和运行。

符合 DCH 的驱动程序二进制文件可使用 [KMDF](https://docs.microsoft.com/windows-hardware/drivers/wdf/index)、[UMDF 2](https://docs.microsoft.com/windows-hardware/drivers/wdf/getting-started-with-umdf-version-2) 或 Windows 驱动程序模型 (WDM)。

符合 DCH 的驱动程序由以下部分组成：

- 基础驱动程序
- 可选组件包
- 可选硬件支持应用

基础驱动程序包含所有核心功能和共享的代码。 可选组件包可以包含自定义项和其他设置。

通常，设备制造商或独立硬件供应商 (IHV) 会编写基础驱动程序。 然后，系统构建者或原始设备制造商 (OEM) 将提供任何可选组件包。

在获得 IHV 认证后，基础驱动程序包就可以部署在所有 OEM 系统上。 由于可以在共享硬件部件的所有系统中使用基准驱动程序包，因此 Microsoft 可以通过 Windows 预览体验成员外部测试广泛地测试基准驱动程序包，而不是将分发局限于特定计算机。

OEM 仅验证它为 OEM 系统提供的可选自定义项。  

## <a name="requirements"></a>要求

若要创建遵循 DCH 设计原则的驱动程序包，请按照以下步骤操作：

*  为驱动程序创建[通用 INF](../install/using-a-universal-inf-file.md)：
    1.  审阅 [Windows 驱动程序包中有效的 INF 部分和指令的列表](../install/using-a-universal-inf-file.md#which-inf-sections-are-invalid-in-a-universal-inf-file)。
    2.  使用 [InfVerif](../devtest/infverif.md) 工具来验证驱动程序包的 INF 文件是否遵循 Windows 驱动程序的声明性 (D) 要求。
*  确保所有不包含核心驱动程序功能的可选组件包都与基础驱动程序包分离。    
*  与驱动程序包关联的硬件支持应用必须通过 Microsoft Store 分发。

## <a name="best-practices"></a>最佳实践

*  如果结合使用 Windows 驱动程序工具包 (WDK) 版本 2004 与最新的 Visual Studio，请将驱动程序项目属性中的“目标平台”值设置为“`Windows Driver`”。  这会自动添加正确的库，并且它会在生成过程中运行正确的 INF 验证和 APiValidator。  若要实现此目的，请执行以下操作：

    1. 打开驱动程序项目属性。
    2. 选择“驱动程序设置”。
    3. 使用下拉菜单将“目标平台”设置为 `Windows Driver`。
   
*  如果 INF 执行依赖于目标平台的任何自定义设置操作，请考虑将其分离形成一个扩展 INF。 可以独立于基础驱动程序包更新扩展 INF，以提高稳健性和可用性。 有关详细信息，请参阅[使用扩展 INF 文件](../install/using-an-extension-inf-file.md)。
*  如果想要提供一个与你的设备兼容的应用程序，请包括 UWP 应用。 有关详细信息，请参阅[硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)。  OEM 可以使用 [DISM - 部署映像服务和管理](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows)预加载此类应用。 或者，用户可以从 Microsoft Store 手动下载此应用。
*  在 [**INF DestinationDirs 部分**](../install/inf-destinationdirs-section.md)中，将目标目录设为 [dirid 13](../install/using-dirids)，使驱动程序可从[驱动程序存储](driver-isolation.md#run-from-driver-store)运行。 此设置不适用于某些设备。


