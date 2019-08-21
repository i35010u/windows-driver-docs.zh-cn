---
title: 如何基于 Windows 版本限制或扩展驱动程序的分发
description: 创建驱动程序提交下限或上限以更改其分发。
ms.topic: article
ms.date: 06/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: be0a92b0c9d72640b4dfaf615be8d8dc35cbb1a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364464"
---
# <a name="how-to-limit-or-expand-a-drivers-distribution-based-on-windows-version"></a>如何基于 Windows 版本限制或扩展驱动程序的分发

合作伙伴有时可能需要扩展或限制某个已提交驱动程序的 OS 分发。  本主题介绍此方面的每个相关的发货标签功能及其使用方法。

## <a name="important-information"></a>重要信息

在开始使用这些功能之前，应熟悉并牢记一些重要原则、术语和定义。

**Windows 更新**：将某个驱动程序发布到特定的 OS 版本（例如 RS1（Windows 10 版本 1607））时，Windows 更新也会将该驱动程序提供给运行 RS2、RS3 及前向版本（Windows 10 版本 1607、1703 和 1709）的系统。 但是，不会将该驱动程序提供给 TH1 或 TH2（Windows 10 版本 1507 或 1511）。 也就是说，驱动程序始终以前向方式提供。 
在发货标签的 PNP 网格中处理 OS 和硬件 ID 组合时，必须记住这一点，这尤其重要。 实际上，就上一示例来说，以前向方式提供驱动程序是指不需将同一硬件 ID 同时发布给 RS2 和 RS3。 Windows 更新会将你的 RS1 发布内容提供给 RS2 及更高版本。  你只需  发布到最低的 OS 版本，即需要在 PNP 网格中将其作为目标的版本。

**动态更新和 OS 下限**：在 Windows **升级**过程中调用 Windows 更新时，后者会按特殊的逻辑来重写客户端报告的当前 OS 版本信息，将其设置为目标功能更新版本。 例如，如果客户端目前使用 10.0.17763（Windows 10 版本 1809），需要升级到 10.0.18362（Windows 10 版本 1903），则动态更新会提供 18362 OS 边界内的驱动程序。 这对于了解何时使用下限功能尤其重要。 有关详细信息，请参阅[了解适用于驱动程序分发的 Windows 更新自动和可选规则](understanding-windows-update-automatic-and-optional-rules-for-driver-distribution.md)。

**提交内容所有者**：HLKx 或 .CAB 驱动程序包的原始提交者。  原始提交者会被授予使用“驱动程序扩展”功能的权限。  共享提交内容的接收者必须通过提交内容所有者来获取某些功能。 

**所需权限**：只有指定为管理员的用户、发货标签所有者和发货标签推广者可以设置驱动程序提交下限和上限。  仅联合研发合作伙伴可以访问基于上限和内部版本号的功能。

**下限和上限类型**：驱动程序仪表板支持两种类型的下限和上限：

<table>
  <thead>
    <tr>
      <th>下限/上限类型</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>基于操作系统版本的类型</td>
        <td>
        <ul>
            <li>选择仅限 TH、RS1、RS2 等。</li>
            <li>适用于向公众发布的驱动程序。</li></ul>
        </td>
    </tr>
    <tr>
      <td>基于内部版本号的类型</td>
      <td>
        <ul>
            <li>仅适用于 Microsoft 联合研发合作伙伴。</li>
            <li>选择仅限五位数的内部版本号，该版本号高于最新发布的 Windows 版本。</li>
            <li>开发适用于未发布 Windows 版本的驱动程序时使用。</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## <a name="setting-an-os-floor"></a>设置 OS 下限

* 当你从 PNP 网格中选择硬件 ID 和 OS 组合时，系统会以隐式方式自动设置一个下限。  这意味着，从 PNP 网格中选择的最低 OS 将会成为隐式下限。  
* 允许的最低 OS 下限一开始取决于提交项的最低认证 OS 级别，或已证明 OS 级别。  如果需要设置的 OS 下限低于这些自动确定的级别，则必须在设置 OS 下限之前进行驱动程序扩展。

OS 下限表示可以将驱动程序分发到的最低 Windows 版本。  若要**提高**隐式下限，使驱动程序只在所选操作系统及更高级别操作系统上提供，请使用此功能。
最常见用例在“驱动程序扩展”部分（即[用例 2](#use-case-2--publishing-an-expanded-submission-to-a-specific-os-level)）介绍。

### <a name="to-set-the-os-floor"></a>设置 OS 下限的步骤

1. 创建一个发货标签并输入详细信息。  有关详细信息，请参阅[将驱动程序发布到 Windows 更新](publish-a-driver-to-windows-update.md)。
2. 在“选择 PNP”网格区域中，  选择至少一个  硬件 ID 和操作系统组合，然后单击“发布”。 
3. 向下滚动到“限制操作系统进行驱动程序分发”部分，勾选“我要限制 OS 进行驱动程序分发”。    仅当你在 PNP 网格中的至少一个项上单击“发布”以后，此选项才会变得可用。 
4. 从“选择最低 OS 版本(下限)”下拉菜单中选取要向其分发驱动程序的最低 OS 版本。 

![列出了 OS 版本的下拉菜单](images/restrict-floor.png)

如果为“OS 下限”选择的值低于 PNP 网格中列出的选项，则会收到以下错误。

![要求用户选择更高 OS 版本的错误消息](images/restrict-floor-error-too-low.png)

## <a name="setting-an-os-ceiling"></a>设置 OS 上限

>[!NOTE]
> 仅允许具有有效业务需求的特定合作伙伴帐户访问“上限”功能。  如有问题，请[联系支持人员](https://go.microsoft.com/fwlink/?linkid=2038065)。

上限表示向 OS 分发驱动程序时，OS 有一个上限。 如果希望驱动程序在已列出的操作系统版本或更低操作系统版本上提供，请使用此选项。

例如，如果选择的“上限”值为 **RS3**（Windows 10 版本 1709），则不会将驱动程序提供给运行 RS4（Windows 10 版本 1803）或更高版本的系统。

>[!IMPORTANT]
>只有在新的 OS 发生影响驱动程序基础功能的重大变更时，才应设置 OS 上限。 当你请求设置 OS 上限时，Microsoft 会要求你提交业务理由。

### <a name="to-set-the-os-ceiling"></a>设置 OS 上限的步骤

1. 创建一个发货标签并输入详细信息。  有关详细信息，请参阅[将驱动程序发布到 Windows 更新](publish-a-driver-to-windows-update.md)。
2. 在“选择 PNP”网格区域中，  选择至少一个  硬件 ID 和操作系统组合，然后单击“发布”。 
3. 向下滚动到“限制操作系统进行驱动程序分发”部分，选择“我要限制 OS 进行驱动程序分发”。    仅当你在 PNP 网格中的至少一个项上单击“发布”以后，此选项才会变得可用。 
4. 从“选择最高 OS 版本(上限)”下拉菜单中选择要向其分发驱动程序的最高 OS 版本。 

![显示 OS 上限选项的对话框](images/restrict-ceiling.png)

>[!NOTE]
>选择的 OS 上限不得高于在 PNP 网格中发布的最高 OS 版本。

如果选择无效，仪表板会显示以下错误。

![指示上限选择无效的错误对话框](images/restrict-ceiling-error.png)

## <a name="driver-expansion-expanding-a-drivers-lowest-os-target"></a>驱动程序扩展：扩展驱动程序的最低 OS 目标

扩展驱动程序的分发时，请注意以下重要信息：

* 只能由**原始提交内容所有者**进行扩展。 共享提交内容的接收者不会看到此选项。 （参见[重要信息](#important-information)。）  
* 每次提交只可执行一次扩展，且不可撤销。  如果已进行过扩展，则“扩展”按钮会灰显。
* 只能对其中的 [INF 制造商部分](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)不使用 \[BuildNumber] *TargetOSVersion* 修饰（例如 NTamd64.10.0...**14393**）的驱动程序进行扩展。
* 只有 Windows 8.1 驱动程序可以**向上**扩展到目标 Windows 10 系统。  Windows 10 驱动程序可以**向下**扩展。
* 扩展不会更改或扩大驱动程序的认证级别。  如果驱动程序是针对 RS5 认证的，扩展不会提供更低的 OS 认证。

有了驱动程序扩展功能，合作伙伴就可以将所有版本的 Windows 10 作为目标。  它还使 Windows 10 系统能够接收 Windows 8.1 驱动程序。

因此，它为提交包内的每个受支持的 INF 创建一个新的“已扩展”  PNP 网格条目（适用于 Windows 10 客户端版本 1506 和 1511 (TH1)  和 Windows Server 2016 x64 (TH1)  ）。    这适用于发货标签中的“共享”和“发布”工作流。 以下屏幕截图显示了 Windows 8.1 驱动程序的扩展按钮和 Windows 10 驱动程序的扩展按钮：

![Windows 8.1 驱动程序的扩展按钮](images/expand-to-win10.png)

![Windows 10 驱动程序的扩展按钮](images/expand-down-th1.png)

例如，以下提交已针对 Windows 10 客户端版本 1809 客户端 x64 (RS5) 进行了认证。  请注意，在扩展后，创建了两个新的“已扩展”  PNP 网格条目。

![一个 UI，显示某个提交扩展了网格条目](images/expansion-pnpgrid-outline.png)

如果此提交中存在多个 INF，则其中的每个 INF 和硬件 ID 会收到相同的全新“已扩展”条目。   例外情况是，如果 [INF 制造商](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)部分使用 *\[BuildNumber] TargetOSVersion* 修饰（例如 NTamd64.10.0...**14393**），  则会跳过这些 INF，不能将其扩展。  这意味着，最终在 PNP 网格中只有部分扩展的 INF 列表。  若要扩展所有 INF 文件，必须编辑 INF，将 *BuildNumber* 删除。  另外，如果没有任何受支持的 INF，则可能根本看不到“展开”选项框。 

有了“已扩展”条目后，即可共享或发布它。 

大多数情况下，你不希望将扩展的驱动程序提供给 TH1 及更高版本，  而是将其提供给介于二者之间的版本。  因此，还需在创建发货标签过程中设置 [OS 下限](#setting-an-os-floor)，这一点必须记住。

下面提供了两个最常见的用例及其实现说明。  我们将使用上面的 toaster 提交作为示例。

## <a name="use-cases-for-limiting-or-expanding-driver-distribution-based-on-os"></a>限制或扩展基于 OS 的驱动程序分发的用例

我们将使用 toaster 示例（显示在上一屏幕截图中）演示其中两个较常见的使用场景，说明如何根据 OS 版本来设置驱动程序分发：

* **用例 1：IHV 将扩展的提交共享给 OEM**  我的 OEM 希望以 RS3 和 RS4 客户端为目标，但我的提交内容仅在 RS5 上进行了认证。  我如何才能为 OEM 合作伙伴启用此功能，让他们能够创建自己的 Windows 更新发货标签？
* **用例 2：将扩展的提交发布到特定 OS 级别**  我想要将 RS5 认证驱动程序发布到 Windows 更新，其目标是 RS3 及更高版本。  如何操作？

### <a name="use-case-1-an-ihv-sharing-an-expanded-submission-to-an-oem"></a>用例 1：IHV 将扩展的提交共享给 OEM

作为提交内容所有者，你是能够扩展提交的唯一人员。

1. 单击“扩展到较低版本的 Windows 10 (从 TH1 开始)”。 
2. 针对 OEM 所需的每个硬件 ID 选择“共享”，  确保包括“Windows 10 客户端版本 1506 和 1511 x64 (TH1)”的“已扩展”条目。    实际上，这是需要与他们共享的唯一 OS 条目，因为 Windows 更新以前向方式提供更新（参见[重要信息](#important-information)）。

![屏幕截图，显示驱动程序未共享，但 OS 处于选中状态](images/pending-share_example1.png)

3. 滚动到页面底部，单击“发布”，完成共享操作。 
4. 通知 OEM 访问此页并阅读[用例 2](#use-case-2--publishing-an-expanded-submission-to-a-specific-os-level)。  

如果已经与合作伙伴共享了一个驱动程序，则可稍后将其扩展并共享其他的已扩展项。  但请注意，原始的共享提交内容会被弃用，合作伙伴只能使用你的最新共享提交内容（若要详细了解已弃用的项，请参阅[撤消/全部撤消](sharing-drivers-with-your-partners.md#revokerevoke-all)部分）。

### <a name="use-case-2--publishing-an-expanded-submission-to-a-specific-os-level"></a>用例 2：将扩展的提交发布到特定 OS 级别

你想要将 Windows 10 RS5 (1809) 驱动程序发布到比 PNP 网格中列出的 OS 版本更低的版本，例如 RS3。  首先需**扩展**提交的内容。  如果此提交是你从 IHV 收到的，则必须由 IHV 完成扩展任务并将扩展的项共享给你（参见[用例 1](#use-case-1-an-ihv-sharing-an-expanded-submission-to-an-oem)）。  

完成驱动程序扩展后，就会为提交包内的每个受支持的 INF 创建一个新的“已扩展”  PNP 网格条目（适用于 Windows 10 客户端版本 1506 和 1511 (TH1)  和 Windows Server 2016 x64 (TH1)  ）。  它将是你需要发布的那些项中的一个。
使用上面的已扩展 toaster 示例时，这是它的正确发布方式，因此其下限为 RS3。

1. 针对 *hid\toaster&col02* 和“Windows 10 客户端版本 1506 和 1511 x64 (TH1)”项选择“发布”。   这样就会将隐式下限设置为 **TH1**。

![屏幕截图，显示提交的版本已选中，其状态设置为“不在 Windows 更新上”](images/expansion-pnpgrid-example1.png)

2. 发货标签现在会在“状态”列中显示“待发布”，如下所示。

![屏幕截图，显示提交的版本已选中，其状态设置为“待发布”](images/expansion-pnpgrid-pending-example1.png)

3. 向下滚动到“限制操作系统进行驱动程序分发”部分，选择“我要限制 OS 进行驱动程序分发”。  
4. 从“选择此驱动程序的最低 OS 版本(下限)”下拉菜单中选择“RS3”。  

![UI，用户已在其中选择最低 OS 版本（下限）](images/restrict-floor-example1.png)

5. 滚动到页面底部，单击“发布”，完成发布请求。 

此驱动程序将会发布，它适用于 RS3 及更高版本的所有 OS 版本。

## <a name="faq"></a>常见问题

### <a name="why-cant-i-check-the-restrict-operating-systems-for-driver-distribution-box"></a>为什么我不能勾选“限制操作系统进行驱动程序分发”框？

请确保已首先针对“选择 PNP”部分的至少一个硬件 ID 条目单击“发布”。  

### <a name="the-expand-to-lower-versions-of-windows-10-starting-from-th1-box-is-greyed-out-or-missing"></a>“扩展到较低版本的 Windows 10 (从 TH1 开始)”框灰显或缺失

如果此框灰显，则表明提交内容已进行过扩展。

如果此框缺失，则表明存在下面的两种情况中的一种：  你不是初始提交内容的所有者，或者你的 INF 包含 BuildNumber 部分。  参见[重要信息](#important-information)。

### <a name="how-can-i-target-a-windows-version-that-is-older-than-my-drivers-certification"></a>如何将早于我的驱动程序认证的 Windows 版本设为目标？

参见[用例 2](#use-case-2--publishing-an-expanded-submission-to-a-specific-os-level)。

### <a name="some-of-my-infs-are-missing-after-expansion--why-cant-i-expand-my-entire-submission"></a>扩展后，我的部分 INF 缺失。  为何我不能扩展我的整个提交？

我们会针对扩展单独评估提交中的每个 INF。 如果其中一个 INF 或所有 INF（参见 [INF 制造商](https://docs.microsoft.com/windows-hardware/drivers/install/inf-manufacturer-section)）使用 *\[BuildNumber] TargetOSVersion* 修饰，我们将无法处理需要扩展的该 INF。 若需扩展提交，则必须先编辑 INF，将 \[BuildNumber] 删除。 不包含 \[BuildNumber] 的 INF 可以成功处理。  有关详细信息，请参阅[重要信息](#important-information)。
