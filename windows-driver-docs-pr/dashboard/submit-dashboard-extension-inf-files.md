---
title: 在 Windows 硬件仪表板中使用扩展 INF
description: 可以在 Windows 硬件开发人员中心为扩展 INF 文件创建发货标签，以便能够像其他提交一样对其进行共享和发布。
ms.topic: article
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: dfccf97d1c2ffdfd0e0d6b7e3c97c102dea5f979
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518156"
---
# <a name="working-with-extension-infs-in-the-windows-hardware-dev-center-dashboard"></a>在 Windows 硬件开发人员中心仪表板中使用扩展 INF

可以在 Windows 硬件开发人员中心为扩展 INF 文件创建发货标签，以便能够像其他提交一样对其进行共享和发布。 本主题介绍打包、提交和发布这些程序包的过程。 有关如何创建和安装扩展 INF 的详细信息，请参阅[使用扩展 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)。

## <a name="requirements-for-publishing-extension-infs-to-windows-update"></a>将扩展 INF 发布到 Windows 更新的要求 
如果要将扩展 INF 发布到 Windows 更新，必须选中发货标签上的自动驱动程序推广复选框。 之所以不能将扩展 INF 作为可选项进行发布，是因为它们未列在设备管理器中，因此最终用户无法启动“更新驱动程序”操作。   若要查看这些复选框，必须先注册[驱动程序外部测试](https://docs.microsoft.com/windows-hardware/drivers/dashboard/driver-flighting)。 

> [!NOTE]
> 发布扩展 INF 文件时，请注意以下事项：
> * 若要让 Windows 更新提供扩展 INF，所有系统都必须至少运行 RS3 [2018 年 1 月更新](https://support.microsoft.com/help/4056892/windows-10-update-kb4056892) (10.0.16299.192)。

## <a name="submitting-and-publishing-extension-infs"></a>提交和发布扩展 INF

此部分介绍如何提交和发布 INF 包。 有关常见错误和常见问题解答的信息，请参阅突出显示的项和常见问题解答。

> [!IMPORTANT]
> Microsoft 建议始终为每个扩展 INF 创建一个单独的提交，以及一个仅包含基准驱动程序提交的单独提交。 在单个提交中发布基准驱动程序和扩展 INF 会导致以下问题：
> * 硬件开发人员中心仪表板会将所有发货标签归类并评估为“扩展驱动程序”。 若要查找属于“扩展”的项，请在开发人员中心搜索框中输入 `@IsExtensionDriver:"True"`。
> * 发布到 Windows 更新后，用户可能不得不多次下载你的驱动程序包：安装基准驱动程序时下载一次，针对 PnP 检测到的每个适用的扩展再下载一次。

### <a name="creating-a-submission-package"></a>创建提交程序包

#### <a name="base-driver-package"></a>基准驱动程序包

1. 照常使用基准驱动程序和扩展 INF 启动 HLK 测试运行。 HLK 结果将用于以下所有程序包创建步骤。 

    ![一个显示 HLK 测试运行的文件输出的图像](images/hlk-result-files.png)

2. 从“Drivers”文件夹中删除扩展 INF 模板项，并且只将基准驱动程序文件添加回 HLK 程序包中，如下所示。

    ![一个显示基准驱动程序文件的图像](images/hlk-result-files2.png)

3. 创建此 HLKx 包并为其签名以制作基准驱动程序包。

    > [!NOTE]
    > 基准驱动程序包必须始终与现有扩展后向兼容

#### <a name="extension-inf-package"></a>扩展 INF 包

1. 使用上面的相同 HLK 结果，选择“程序包” > “替换驱动程序”

    ![一个显示 HLK 中的“替换驱动程序”选项的图像](images/hlk-replace-driver.png)

2. 将扩展 INF 添加到具有任何引用的二进制文件的驱动程序文件夹。 如果有多个扩展 INF，则只能添加一个文件。 

3. 创建此新 HLK 程序包并为其签名。 这将是扩展 INF 包。

4.  对每个扩展 INF 重复此过程，每次都删除驱动程序文件夹内容。

### <a name="submitting-your-packages-to-the-hardware-dev-center-dashboard"></a>将程序包提交到硬件开发人员中心仪表板

为上面创建的每个程序包都创建一个新的提交，并将其上传到硬件开发人员中心。  以后，为需要共享或发布的项创建发货标签。 有关详细信息，请参阅 [Create a new hardware submission](https://docs.microsoft.com/windows-hardware/drivers/dashboard/create-a-new-hardware-submission)（创建新硬件提交）和 [Manage driver distribution with shipping labels](https://docs.microsoft.com/windows-hardware/drivers/dashboard/manage-driver-distribution-by-submission)（使用发货标签管理驱动程序分发）。

#### <a name="extensionid"></a>ExtensionID

ExtensionID 是你生成的用于驱动程序沿袭标识和版本控制的 GUID。 它描述硬件设备部件或部件系列，并且会向已提交它的 SellerID [自动注册](https://blogs.msdn.microsoft.com/windows_hardware_certification/2017/11/08/hardware-dev-center-now-automatically-registers-extension-ids/)。 此 SellerID 的所有者负责跟踪 ExtensionID 的使用和映射，类似于 CHID 管理。 

例如，为新系统部件创建 ExtensionID 时：

* ExtensionID 所有权将分配给 SellerID。
* 组织中使用部件或部件系列的每个系统项目都将共享相同的 ExtensionID。
* ExtensionID 在部件的生命周期中将保持不变。

> [!NOTE]
> * 如果你使用与 SellerID 不相关的 ExtensionID，则硬件开发人员中心仪表板将拒绝你的提交，并通知你该 ExtensionID 已属于另一个组织：
> * 对于给定的设备，会针对每个唯一的 ExtensionID 值只安装一个扩展 INF。 因此，如果设备具有多个扩展 INF，则每一项都将需要一个新的 ExtensionID。  这也意味着，如果两个扩展 INF 面向具有不同 ExtensionID 的相同设备，那么将应用这两个扩展 INF。 有关详细信息，请参阅 [Using an Extension INF file](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)（使用扩展 INF 文件）。
>
> 如果你的组织管理另一个组织的项目和提交，请注意以下各项：
> * ExtensionID 所有权已分配给完成提交的 SellerID。 
> * 通过使用其他组织的 SellerID，你可以使用其 ExtensionID。
> * 若要使用组织的 SellerID，需要针对部件或部件系列创建自己的 ExtensionID。

应该为 Extension INF 的初始版本生成一个新的 ExtensionID（即第一次自定义并提交扩展 INF）。 这包括第一次收到新设备的新共享发货标签。 Visual Studio 在“工具”>“创建 GUID”中包含一个 GUID 创建实用程序，但是如果任何联机 GUID 生成工具与注册表格式匹配，那么该工具应该可以工作，如下所示。

![一个显示在 Visual Studio 中创建 GUID 屏幕的图像](images/guid-formatting.png)

若要更新已持续发布的扩展 INF，请保持 ExtensionID 不变并递增 [DriverVer 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)所指定的版本和/或日期。 系统会（按该顺序）使用驱动程序日期和驱动程序版本，以便区分具有相同 ExtensionID 的多个扩展 INF。

### <a name="publishing-an-extension-inf"></a>发布扩展 INF

若要发布扩展 INF 提交，请按照 [Publish a driver to Windows Update](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)（将驱动程序发布到 Windows 更新）中的步骤进行操作。 请确保选择两个自动驱动程序推广选项，并且扩展 INF 具有特定目标。 

![一个显示自动驱动程序推广的图像](images/automatic-driver-promotion-options.png)

如果未看到这些驱动程序推广选项，则可能需要注册[驱动程序外部测试](https://docs.microsoft.com/windows-hardware/drivers/dashboard/driver-flighting)。

所有扩展 INF 在完成驱动程序外部测试过程以后才能通过 Windows 更新进行分发。 外部测试成功后，将向零售系统提供文件。 如果加入 Windows 预览体验成员计划，则能在此阶段更快地访问驱动程序。

## <a name="extension-inf-targeting-and-ranking-differences"></a>扩展 INF 定向和排名差异

由于扩展是特定设备的自定义项，因此它们必须始终面向特定目标。  使用扩展 INF 定向时，请遵循以下指南：
* 如果可能，扩展 INF 文件必须具有由 4 部分组成的硬件 ID (HWID)。 
* 除了具有由 4 部分组成的 HWID 之外，还必须将 CHID 添加到扩展 INF 的发货标签。
* 对于没有由 4 部分组成的 HWID 的部件和部件系列，需要在发货标签上进行 CHID 定向。

此定向信息对于通过 Windows 更新 (WU) 进行分发期间准确评估扩展 INF 至关重要。 在以下两个阶段中，WU 会评估驱动程序：

1. 适用性阶段（此时 WU 会生成一个适用于给定系统的驱动程序列表）。
2.  排名阶段（在此阶段，Windows PnP 和 WU 会确定要安装列表中的哪个驱动程序）。

一般情况下，关于扩展 INF 的排名/定向有以下几个关键原则：  

* 扩展 INF 的 ExtensionID 不用于适用性 - 仅用于沿袭和版本标识。

* WU 将为每个适用的扩展 ID 提供排名最高的扩展驱动程序（PnP 将为其安装此驱动程序）。

* 扩展驱动程序仅按照 DriverVer 指令中所包含的日期和版本进行排名。 WU 和 PnP 都使用此项。  有关详细信息，请参阅 [INF Version Section](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)（INF 版本部分）和 [INF DriverVer directive](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)（INF DriverVer 指令）。
    * 注意，对于扩展驱动程序，PnP 和 WU 不考虑功能或标识符分数（即 2 部分与 4 部分）。

* 在 WU 上对扩展驱动程序排名时不使用 CHID 信息（即，不能“阻止”具有 CHID 定向的其他扩展驱动程序）。

* 有关 Windows 操作系统中的驱动程序选择和定向的信息，请参阅 [Using an Extension INF file](https://docs.microsoft.com/windows-hardware/drivers/install/using-an-extension-inf-file)（使用扩展 INF 文件）

## <a name="faq"></a>常见问题

### <a name="driver-development"></a>驱动程序开发

**我们每次更新基准驱动程序时是否都需要更改 ExtensionID？**

不，更新基准驱动程序时，应该保持相同的扩展 ID。  ExtensionID 用于版本比较和驱动程序沿袭标识。  它不应在驱动程序沿袭中发生变化。 

### <a name="manufacturing"></a>制造

**我们是否可以为制造目的将 IHV 提供的扩展 INF 与其 ExtensionID 配合使用？**

否。 如果你计划对扩展的服务方面负责，则必须在制造期间使用自己的扩展 INF 和 ExtensionID。  


### <a name="driver-updates"></a>驱动程序更新

**每次更新和发布基准驱动程序包时，我们是否需要将更新的扩展 INF 发布到 Windows 更新？**

不，一定不要这么做。  基准驱动程序包必须始终与现有扩展后向兼容。
 
**向最终用户的系统发布并应用更新的基准驱动程序时会发生什么情况？** 

应用基准驱动程序更新时，如有必要，将评估和应用当前安装的扩展 INF。 如果没有安装扩展 INF，则 Windows 更新将下载最新的适用版本。

**当我们将操作系统更新到最新版本时，是否需要发布更新的扩展 INF 或 ExtensionID？**

不需要，现有的 ExtensionID 和扩展 INF 将继续工作。 

**如果两个系统的自定义项相同，那么这两个系统是否可以共享相同的扩展 INF？**

是。  如果多个系统使用相同的设置，或者如果你想要在更广泛的一组设备中自定义设置，则一个扩展 INF 就足够了。  为此，需将由 4 部分组成的适用硬件 ID 添加到扩展 INF 中。 有关详细信息，请参阅“Using an Extension INF File”（使用扩展 INF 文件）。

## <a name="related-pages"></a>相关页面

### <a name="hardware-dev-center"></a>硬件开发人员中心 

* [硬件提交](hardware-certification-submissions.md)

* [驱动程序外部测试](driver-flighting.md) 

* [使用发货标签管理驱动程序分发](driver-flighting.md)

* [发布到 Windows 更新](publish-a-driver-to-windows-update.md)

### <a name="windows-drivers"></a>Windows 驱动程序：

* [Using a Universal INF File](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)（使用通用 INF 文件）

* [通用驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)

* [Using a component INF file](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-component-inf-file)（使用组件 INF 文件）

* [How windows ranks drivers](https://docs.microsoft.com/windows-hardware/drivers/install/how-setup-ranks-drivers--windows-vista-and-later-)（Windows 如何对驱动程序排名）
