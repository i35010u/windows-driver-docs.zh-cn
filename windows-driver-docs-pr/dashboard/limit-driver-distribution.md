---
title: 驱动程序分发扩展
description: 创建驱动程序提交下限或上限以更改其分发。
ms.topic: article
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: dbcd3bf1e34fe324f04c42819476a2d54c5bfaba
ms.sourcegitcommit: 71c90354f7e2d88498e28f74fb1b34748edf82ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2019
ms.locfileid: "66491759"
---
# <a name="limiting-driver-distribution-by-windows-versions"></a>按 Windows 版本限制驱动程序分发

IHV、OEM 和 ODM 通常需要在 Windows 更新中将驱动程序分发更改为特定的 Windows 版本范围。 例如，驱动程序可能：

* 在指定范围的版本中有已知问题。

* 需要部署以修复过去的 Windows 版本中的问题，同时当前驱动程序分发到当前版本。

* 将其分发扩展到早期、当前或更高的 Windows 版本中。

这些分发范围是由**下限**和**上限**定义的。 下限表示驱动程序将分发到的最低 Windows 版本，而上限则表示最新版本。 通过添加下限和上限可限制驱动程序的分发。 对于以下驱动程序提交格式，下限和上限是在合作伙伴中心的[发货标签](https://docs.microsoft.com/windows-hardware/drivers/dashboard/manage-driver-distribution-by-submission)中指定的：

* .HLKX
* .HCKX
* .CAB

> [!NOTE]
> 只有管理员、发货标签所有者和发货标签推广者可以设置驱动程序提交下限和上限。

## <a name="floor-and-ceiling-types"></a>下限和上限类型

下限和上限适用于更高、早期或当前 Windows 操作系统版本。
HDC 仪表板支持两种类型的下限和上限：

| 下限/上限类型 | 描述 |
| -- | -- |
| 基于操作系统版本的类型 | <ul><li>用于将驱动程序扩展或限制为除认证的 Windows 操作系统版本外的其他 Windows 版本。</li><li>适用于向公众发布的驱动程序。</li></ul> |
| 基于内部版本号的类型 | <ul><li>开发适用于更高和未发布 Windows 版本的驱动程序时使用。 </li><li>仅适用于 Microsoft 联合研发合作伙伴。</li></ul> |

## <a name="setting-floors-and-ceilings-for-your-driver-distribution"></a>为驱动程序分发设置上限和下限

1. 创建一个发货标签，并输入你的详细标签名称、发布者和目标。 有关详细信息，请参阅[将驱动程序发布到 Windows 更新](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)。

2. 在“选择 PNP”  中，选择你要发布到的硬件 ID 和操作系统组合。 请注意，可以为每个硬件 ID 设置下限，但上限适用于同一发货标签内的所有 ID。 此外，你选择的最旧的操作系统将自动选择成为你的标签下限。 

## <a name="restricting-driver-distribution-using-floors-and-ceilings"></a>利用上限和下限来限制驱动程序的分发

限制驱动程序的分发使你可以设置操作系统 (OS) 的最低和最高级别。 对于证明提交，我们会将你在提交时选择的 OS 作为初始最低级别 OS。 最低 OS 级别不能低于驱动程序认证的 OS 级别。 你必须先使用扩展（描述如下）使其低于初始最低级别。

### <a name="os-flooring"></a>OS 下限
*（最低 OS 要求）*

当你希望驱动程序只在已列出的操作系统或更高级别的操作系统上提供时，请使用此选项。 例如，选择 RS4 下限意味着只有运行 Windows 10 1803 (RS4) 或以上级别的系统才可被提供此驱动程序。

### <a name="os-ceiling"></a>OS 上限  
*（最高 OS 要求）*

*注意：对此功能的访问受限。*

> [!IMPORTANT]
> * 只有在新的 OS 发生影响驱动程序基础功能的重大变更时，才应设置 OS 上限。 申请设置 OS 上限时需要提供业务理由。
> * 上限选项仅对面向 Windows 10 的硬件 ID 启用，并且仅当在“选择 PNP”  选择区域中单击“发布”后才会启用。
> * 你选择的上限应高于你所做的 PNP 选择。

在你希望驱动程序只在已列出的操作系统或更低级别的操作系统上提供时，请使用此选项。 例如，在 Windows 10 1607 RS1 认证驱动程序上选择 RS3 上限意味着驱动程序不会被提供给运行 Windows 10 1803 (RS4) 或以上级别的系统。

最低 OS 级别由产品认证 OS 级别或已证明 OS 级别决定。  如果你需要更低级别，可使用驱动程序扩展，描述如下。

## <a name="driver-expansion"></a>驱动程序扩展

> [!IMPORTANT]
> 扩展驱动程序的分发时，请注意：
> * 共享提交不能扩展。 你只能扩展你提交的驱动程序。
> * 每次提交只可执行一次扩展，且不可撤销。 仅在绝对有必要时扩展驱动程序的分发。
> * 扩展只能进行驱动程序，你[ **INF 制造商部分**](../install/inf-manufacturer-section.md)会使用 [BuildNumber] *TargetOSVersion*修饰。
> * 所有与扩展提交关联的发货标签将列出新的 PNP HWID，可用于定位 **Windows 10 客户端版本 1506 和 1511 (TH1)** 。 
> * 这些新建项目的认证级别将显示为“扩展”。
> * 只有 Windows 8.1 驱动程序可以向上扩展到目标 Windows 10 系统。  
> * 扩展不会对驱动程序进行重新签名，或更改驱动程序的认证级别。

驱动程序提交中的扩展流程使该驱动程序可以将低于产品认证级别或已证明 OS 级别的操作系统作为目标。 它还使 Windows 10 系统能够接收 Windows 8.1 驱动程序。  就 Windows 10 来说，如果 [**INF 制造商部分**](../install/inf-manufacturer-section.md)使用 [BuildNumber] *TargetOSVersion* 修饰（例如 NTamd64.10.0...**14393**），则**扩展**不会发生。

例如，如果希望能够将 Windows 10 RS3 (1709) 驱动程序提供给 Windows 10 RS1 (1607)，请单击“展开”  。 这将为你的 INF 中列出的每个 HWID 创建一个新的基线操作系统选择项。  此基线显示为“Windows 10 客户端版本 1506 和 1511 (TH1)”  并且在“认证”部分中显示“已扩展”。   基线 OS 始终是 Windows 10 1506 (TH1) 并且是我们的起始 OS 目标点。

![驱动程序扩展选项的屏幕截图。](images/new-pnp-nodes.png)

若要将 OS 下限提高到 RS1，请使用上面提到的下限功能。  选择所需的**已扩展** HWID，然后单击“发布”。  

> [!NOTE]
> 在上面的示例中，不需要发布列出了 Windows 10 RS3 的任何 HWID。  这是因为你将设置 OS 下限 RS1。  **已扩展**的驱动程序将正确提供给高于最低起点的所有操作系统。  这意味着它将提供给 RS1、RS2、RS3，等等。如果在选择了以 Windows 10 RS3 (1709) 为目标的驱动程序时尝试将下限设置为 RS1，则会导致一个错误，指示你选择较高的 OS 下限目标。 

## <a name="faq"></a>常见问题

**何时需要为已发布的 Windows 版本指定下限或上限？**

*要阻止预先存在的驱动程序发布到将来的 Windows 版本中时。例如，当开发面向未发布的 Windows 版本的替换驱动程序时。*

**何时需要为联合研发的驱动程序指定下限和/或上限？（即将推出）**

*如果你的驱动程序包含目前正在开发中的 Windows 版本中的依赖项，你可能需要指定该 Windows 版本作为下限。*

**如何将早于我的驱动程序认证的 Windows 版本设为目标？**

 参阅“驱动程序扩展”部分中的上述示例。

**为何我不能扩展我的整个提交？**

*提交中的每个 INF 都会针对扩展单独进行评估。如果其中一个 INF 或所有 INF 的 [**INF 制造商部分**] 使用 [BuildNumber] TargetOSVersion 修饰，我们将无法处理扩展的该 INF。若需扩展提交，则必须先编辑 INF，将 [BuildNumber] 删除。不包含 [BuildNumber] 的 INF 可以成功处理。*
