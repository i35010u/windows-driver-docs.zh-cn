---
title: 逐步推出
description: 逐步推出通过监视部署期间的遥测数据并根据要求加快和减慢发布速度，来确保每个系统的最佳驱动程序体验。
ms.author: webreidi
ms.topic: article
ms.date: 03/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0b51bb20af44f5e3adfcd2b65fad05f51e425571
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88253023"
---
# <a name="gradual-rollout"></a>逐步推出

逐步推出可以监视遥测数据以确保尽量为客户提供最佳体验，其目的是确保 Windows 生态系统为每个系统提供最适合的驱动程序。 如果某个驱动程序在逐步推出阶段出现不正常的迹象，Microsoft 可以选择**暂停**该驱动程序的分发以展开调查，和/或寻求适当的补救措施，包括 Microsoft 发起的驱动程序取消（过期）。 

>[!NOTE]
> - 逐步推出的驱动程序仅对运行 Windows 10 版本 1709 和更高版本的系统可见。

## <a name="main-concepts-of-gradual-rollout"></a>逐步推出的主要概念

合作伙伴应该了解逐步推出过程的两个不同方面。  它们是：

- 30 天**监视**期
  - 30 天监视期从驱动程序受到限制的第一天开始，在大约 30 天后结束。 此监视期不会影响驱动程序的 WU（Windows 更新）状态。
- **驱动程序限制**期
  - Microsoft 会针对每个符合条件的驱动程序完成风险评估，并为该驱动程序分配发布限制曲线。 驱动程序风险是根据多种因素评估的，包括但不是局限于外部测试覆盖率和零售群体。
  - 下面是一些典型的驱动程序发布限制曲线：
    - 立即限制到 100% 的 Windows 零售群体 
    - 通过 1% 到 100% 的 Windows 零售群体进行限制 
    - 使用一组高度活跃的合格初始群体进行限制，并且在进展到 1% 至 100% 的 Windows 零售群体之前，保证均匀采用按硬件 ID (HWID) 和计算机硬件 ID (CHID) 组合监管的每个目标群集
  - 当限制百分比达到 100% 时，运行 **Windows 10 版本 1709 和更高版本**的所有系统上的 WU 都会完全推出该驱动程序。 Microsoft 会继续**监视** 30 天期限剩余时间的发布。

请注意，在整个过程中，发货标签的状态将保持为“逐步推出”。  这是正常情况，驱动程序将在 Windows 更新中提供。

 ![驱动程序提交进度阶段的屏幕截图：已创建、验证、更新生成、Microsoft 审批、逐步推出、发布和完成](images/gradual-rollout-phases.png)

 在下图中可以看到，可能不需要 30 天即可达到驱动程序限制百分比 100%。 但是，整个逐步推出阶段需要花费大约 30 天才能从头到尾地完成驱动程序的**状态**过渡。 

 ![显示三个示例驱动程序以不同的速率达到 100% 限制百分比的图表：1、15 和 9 天。 在整个 30 天期限内，所有驱动程序都会受到监视。](images/gradual-rollout-chart.png)

## <a name="partner-dev-center-changes"></a>合作伙伴开发人员中心更改

在前面的图像中可以看到，**逐步推出**在进度栏上现在显示为新的“发货标签”阶段。 仪表板在进度栏下方的说明文本中显示驱动程序的“限制百分比”，另外还会显示一个“取消”按钮。  

 ![逐步推出状态指示器下面的文本屏幕截图。 该文本指出标签针对 100% 的符合条件的群体。 此外，现在可以使用“取消”按钮。](images/gradual-rollout.png)

当驱动程序处于“Microsoft 审批”或“逐步推出”阶段时，发货标签将会锁定以进行任何编辑或修改。   但是，此时可以**取消**发货标签。 单击“取消”按钮会结束整个发货标签（过期）。  请注意，仅当驱动程序处于“Microsoft 审批”或“逐步推出”阶段时，“取消”按钮才起作用。   

## <a name="systems-included-in-the-throttled-percentages"></a>限制百分比涵盖的系统

当驱动程序被限制时，Microsoft 会根据目标受众基线，使用**整个 Windows 10 版本 1709 和更高版本的零售群体**。  在限制完成并且发货标签进入“完成”步骤后，使用 Windows 10 版本 1703 和更低版本的设备会收到该驱动程序。 

## <a name="driver-throttling-assessments"></a>驱动程序限制评估

### <a name="rules-that-define-which-release-throttle-curve-a-driver-gets-assigned-with"></a>一些规则，用于定义根据哪一发布限制曲线分配驱动程序 ###

限制曲线与风险评估紧密相关。 驱动程序风险是根据多种因素评估的，包括但不是局限于外部测试覆盖率和零售群体。

可选的驱动程序通常会立即限制为 100%，但受最多 30 天的监视。 

已发布到测试注册表项后的驱动程序将立即限制为 100%，并免除 30 天的监视。 

### <a name="rules-that-define-when-a-rollout-should-automatically-pause"></a>定义何时自动暂停推出的规则

如果驱动程序不符合 Microsoft 质量检查要求，Microsoft 会暂停逐步推出过程。  在决定是否要将驱动程序递进到下一限制级别时，Microsoft 也会使用相同的质量检查。  

已暂停的驱动程序会显示限制百分比 **0%** 。

暂停后，如果功能团队或 OEM 完成了调查，Microsoft 将继续实施推出过程。

>[!NOTE]
>驱动程序船坞管理员也有权根据其他遥测信号暂停推出。

### <a name="rules-that-define-when-releasestatus-should-be-set-to-complete"></a>定义何时将“发布状态”设置为“完成”的规则  

在 30 天监视期结束后，将发布发货标签进行编辑。 合作伙伴开发人员中心仪表板上的发货标签状态将递进到“完成”。 

## <a name="faq"></a>FAQ

### <a name="when-will-the-30-day-monitoring-period-start-and-what-should-we-expect"></a>30 天监视期何时开始，预期会有哪些动作？

所有受限制的驱动程序，不管它们的限制百分比最初是 1% 还是 100%，都会受到监视至少 30 天。 驱动程序在以任何受限制状态发布给零售群体后，立即开始进入监视期。

在此 30 天推出和监视阶段，发货标签将被锁定以进行任何编辑。 可以选择发货标签上的“取消”按钮取消发货标签。

如果 Microsoft 需要**暂停**驱动程序进行调查，此 30 天期限可能会延长。

### <a name="is-my-driver-available-on-wu-during-gradual-rollout"></a>在逐步推出期间，WU 中是否会提供我的驱动程序？

驱动程序将在 WU 中提供，但仅适用于运行 Windows 10 版本 1709 和更高版本的系统。

在发货标签进入“完成”阶段之前，运行 Windows 10 版本 1703 和更低版本的系统无法获取该驱动程序。 

对于“自动/关键”驱动程序，可以使用设备管理器手动触发驱动程序更新，不管驱动程序的限制百分比是多少。  这适用于运行 Windows 10 版本 1709 和更高版本的系统。 在驱动程序进入“完成”阶段之前，测试人员、支持人员和各种 OEM 审核工具可以使用此策略来获取该驱动程序。  但是，如果暂停了某个“可选”的驱动程序，则无法通过设备管理器使用该驱动程序。 

当驱动程序的限制百分比达到 100% 时，该驱动程序会在 WU 中推出，可供运行 Windows 10 版本 1709 和更高版本的所有合格系统使用，即使监视阶段尚未完成。

### <a name="how-will-microsoft-notify-an-owner-if-a-driver-is-paused-or-cancelled"></a>如果暂停或取消了驱动程序，Microsoft 如何告知所有者？

驱动程序暂停或取消通知只会通过发货标签提供。

### <a name="how-can-we-expedite-this-process-if-we-have-a-critical-business-need"></a>如何加速此过程以解决关键的业务需求？

在提交加速请求之前，请查看发货标签并检查 UI 文本消息，以确定限制百分比是否达到了 100%。 如果达到了 100%，则表示驱动程序已在 WU 中推出，可供运行 Windows 10 版本 1709 和更高版本的所有系统使用。

接下来，请验证并测试是否可以从设备管理器接收该驱动程序。

仅当存在关键业务需求或者想要使用运行 Windows 10 版本 1703 或更低版本的计算机时，才提交加急请求。

若要提交要加急的[支持请求](https://developer.microsoft.com/windows/hardware/support)，请包含你的业务理由。 在 Windows 硬件工程支持页上，请务必使用你的硬件开发人员中心/合作伙伴中心登录凭据登录，使我们能够正确地将请求链接到适当的合作伙伴帐户：

1. **首先**使用硬件开发人员中心帐户登录，然后
2. 转到 [https://developer.microsoft.com/windows/support](https://developer.microsoft.com/windows/support)。
3. 依次选择“联系我们”、“仪表板问题”，然后从下拉菜单中选择“硬件提交和签名(所有 OS 版本)”。   