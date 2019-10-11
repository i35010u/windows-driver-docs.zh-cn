---
ms.assetid: E109BD80-F9CB-4F1F-A6FD-1142E27EC6AD
title: 通用 Windows 驱动程序入门
description: 使用通用 Windows 驱动程序，可以创建一个在多种设备类型（从嵌入式系统到平板电脑和电脑）上运行的驱动程序。
ms.date: 04/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: e09e700906f5fc86f6e100d5ab1c6a60fc0a69c3
ms.sourcegitcommit: 0b38c5075d85ede328bf9901b0d36e84ec0e3d66
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2019
ms.locfileid: "71826520"
---
# <a name="getting-started-with-universal-windows-drivers"></a>通用 Windows 驱动程序入门

通用 Windows 驱动程序使开发人员能够创建在多种设备类型（从嵌入式系统到平板电脑到台式电脑）上运行的单个驱动程序包。

通用 Windows 驱动程序包包含一个 INF 文件和在[基于通用 Windows 平台 (UWP) 的 Windows 10 版本](windows-10-editions-for-universal-drivers.md)上安装和运行的二进制文件。 它们还在共享一组公共接口的其他 Windows 10 版本上安装和运行。


驱动程序二进制文件可使用 [KMDF](../wdf/index.md)、[UMDF 2](../wdf/getting-started-with-umdf-version-2.md) 或 Windows 驱动程序模型 (WDM)。

通用驱动程序由以下部分组成：
- 基础驱动程序 
- 可选组件包 
- 可选硬件支持应用 

基础驱动程序包含所有核心功能和共享的代码。 可选组件包可以包含自定义项和其他设置。

通常，设备制造商或独立硬件供应商 (IHV) 会编写基础驱动程序。 然后，系统构建者或原始设备制造商 (OEM) 将提供任何可选组件包。

IHV 遵循驱动程序包隔离的设计最佳做法，以确保驱动程序提供可靠和稳健的维护操作  。

IHV 认证了基础驱动程序后，该驱动程序便可以在所有 OEM 系统上部署。 由于可以在共享一个硬件部件的所有系统中使用一个基础驱动程序，因此 Microsoft 可以通过使用 Windows 预览体验成员*驱动程序外部测试*广泛地测试该基础驱动程序，而不是将分发局限于特定计算机。

IHV 认证基准驱动程序包后，可以在所有 OEM 系统上部署该驱动程序。 由于可以在共享硬件部件的所有系统中使用基准驱动程序包，因此 Microsoft 可以通过 Windows 预览体验成员外部测试广泛地测试基准驱动程序包，而不是将分发局限于特定计算机。 

OEM 仅验证它为 OEM 系统提供的可选自定义项。

通用驱动程序通过 Windows 更新来分发，硬件支持应用通过 Microsoft Store 来分发。

## <a name="design-principles"></a>设计原则

编写通用驱动程序包时，需要考虑以下四个设计原则：

* 声明性 **(D)** ：仅使用声明性 INF 指令安装驱动程序。 请勿包括共同安装程序或 RegisterDll 函数。

* 组件化 **(C)** ：特定于版本的、特定于 OEM 和可选的驱动程序自定义项独立于基础驱动程序包。 因此，可以独立于自定义项为仅提供核心设备功能的基础驱动程序设定目标、进行外部测试和提供服务。

* 硬件支持应用 **(H)** ：与通用驱动程序关联的任何用户界面 (UI) 组件都必须打包为硬件支持应用 (HSA) 或预安装在 OEM 设备上。  HSA 是与驱动程序配对的可选设备特定应用。 此类应用程序可以是[通用 Windows 平台 (UWP)](https://docs.microsoft.com/windows/uwp/get-started/universal-application-platform-guide) 或[桌面桥](https://docs.microsoft.com/windows/uwp/porting/desktop-to-uwp-root)应用。  必须通过 Microsoft Store 分发和更新 HSA。  有关详细信息，请参阅[硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)和[硬件支持应用 (HSA)：适用于应用开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-app-developers.md)。

* 通用 API 合规性 **(U)** ：通用驱动程序包中的二进制文件仅调用基于 UWP 的 Windows 10 版本中所包含的那些 API 和 DDI。 这些 DDI 在对应的文档参考页上被标记为“通用”  。 INF 文件仅使用通用 INF 语法。

此外，通用驱动程序还受益于驱动程序包隔离原则。  可在[驱动程序包隔离](driver-isolation.md)页中找到关于如何遵循这些最佳做法的详细指南。

在此文档中，我们使用 **DCHU** 首字母缩略词来表示这些原则。 可以在下文中找到关于如何使驱动程序包符合 DCHU 的指南。
此外，请查阅[通用驱动程序方案](universal-driver-scenarios.md)，其中介绍了 [DCHU 通用驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)如何应用 DCHU 设计原则。

## <a name="requirements"></a>要求

编写通用驱动程序包时，请按照下列步骤进行操作：

*  为驱动程序创建一个[通用 INF 文件](../install/using-an-extension-inf-file.md)：
    1.  查看[通用驱动程序包中有效的 INF 部分和指令的列表](../install/using-a-universal-inf-file.md#which-inf-sections-are-invalid-in-a-universal-inf-file)。
    2.  使用 [InfVerif](../devtest/infverif.md) 工具验证驱动程序包的 INF 文件是否为通用。
*  使用 [ApiValidator 工具](validating-universal-drivers.md)验证二进制文件调用的 API 是否对通用驱动程序包有效。

## <a name="best-practices"></a>最佳做法

*  如果正在 Visual Studio 中使用 Windows 驱动程序工具包 (WDK)，请将驱动程序项目属性中的“目标平台”  值设置为 `Universal`。  这将自动添加正确的库，并且会在生成过程中运行通用 INF 验证和 APiValidator。  要实现此目的，请执行以下操作：

    1. 打开驱动程序项目属性。
    2. 选择“驱动程序设置”  。
    3. 使用下拉菜单将“目标平台”  设置为 `Universal`。

* 驱动程序包隔离：

  * 若要最大程度提高通用驱动程序的可靠性和可维护性，请确保驱动程序遵循驱动程序包隔离原则 
  * 驱动程序包隔离是一个新概念，可允许驱动程序变得独立，并且对于 OS 更改具有稳健性
  * 在[驱动程序包隔离](driver-isolation.md)页查看更多详细信息
    
*  如果 INF 执行依赖于目标平台的任何自定义设置操作，请考虑将其分离形成一个扩展 INF。 可以独立于基础驱动程序包更新扩展 INF，以提高稳健性和可用性。 有关详细信息，请参阅[使用扩展 INF 文件](../install/using-an-extension-inf-file.md)。
*  如果想要提供一个与你的设备兼容的应用程序，请包括 UWP 应用。 有关详细信息，请参阅[硬件支持应用 (HSA)：适用于驱动程序开发人员的步骤](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md)。  OEM 可以使用 [DISM - 部署映像服务和管理](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows)预加载此类应用。 或者，用户可以从 Microsoft Store 手动下载此应用。
*  在 [**INF DestinationDirs 部分**](../install/inf-destinationdirs-section.md)中，将目标目录设为 [dirid 13](../install/using-dirids.md)，使驱动程序可从[驱动程序存储](https://docs.microsoft.com/en-us/windows-hardware/drivers/install/driver-store)运行。 此设置不适用于某些设备。
*  提交通用驱动程序包用于在 Windows 硬件兼容性计划中进行认证。 有关详细信息，请参阅以下主题：

   *  [创建新硬件提交](../dashboard/create-a-new-hardware-submission.md)
   *  [在 Windows 硬件开发人员中心仪表板中管理硬件提交](../dashboard/manage-your-hardware-submissions.md)
   *  [获取由 Microsoft 签名的适用于多个 Windows 版本的驱动程序](../dashboard/get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)
   *  [驱动程序外部测试](../dashboard/driver-flighting.md)
