---
title: 逐渐推出的驱动程序分发
description: 逐渐推出通过在部署过程中监视遥测，确保每个系统的最佳驱动程序体验，从而加快并拖慢发布所示。
author: sillykeith
ms.author: keithke
ms.topic: article
ms.date: 06/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 996214fcc27f5d1a4fb055b1d251d32a42af358a
ms.sourcegitcommit: e542212bb5e7aba06b9e005e9b63c438404d5643
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66721855"
---
# <a name="gradual-rollout"></a>逐步推出

逐渐推出的目标是确保 Windows 生态系统具有最适合的驱动程序可用于每个系统通过监视遥测，以确保客户获得尽可能最佳的体验。 驱动程序出现不正常逐渐推出阶段，Microsoft 可能会选择到**暂停**调查驱动程序分发和/或查找适当的补救，包括 Microsoft 启动驱动程序取消 （_到期_)。

>[!NOTE]
> - 逐步推出此功能的驱动程序是可见仅与系统运行 Windows 10 版本 1709年及更高版本。
> - 最终，所有提交到 Windows 更新的驱动程序会通过逐步实施。

## <a name="main-concepts-of-gradual-rollout"></a>逐渐推出的主要概念

有两个不同方面的合作伙伴应了解逐步推出过程。  这些是：

- 30 天**监视**段
  - 驱动程序将受到限制，并结束大约 30 天后的第一天开始 30 天监视过程。 此监视期间不会影响您的驱动程序 WU 状态。
- **驱动程序限制**段
  - 限制范围是从 1%到 100%的零售 Windows 总体。
  - 自动化规则控制的百分比进度。
  - 受限制的百分比为 100%时完全运行的所有系统上 WU 实时**Windows 10 版本 1709年及更高版本**。  Microsoft 将继续**监视器**30 天内的其余部分的版本。

请注意，在此整个过程中，保留的发货标签的状态作为**逐步推出**。 这是正常的并且您的驱动程序是在 Windows Update 上可用。

 ![驱动程序提交的进度阶段的屏幕截图：创建，验证更新生成、 Microsoft 批准、 逐步实施、 发布和最终完成](images/gradual-rollout-phases.png)

 您可以在以下图表中看到的不可能需要 30 天，以达到 100%的驱动程序限制百分比。 但将需要花费*有关*后 30 天开始到结束您的驱动程序**状态**到过去的逐步推出阶段的进度。

 ![显示进度的三个示例驱动程序达到 100%以不同速率受到限制的图表：1、 15 日到 9 天。 所有会在 30 天内进行监视。](images/gradual-rollout-chart.png)

## <a name="partner-dev-center-ui-and-usability-changes"></a>合作伙伴开发人员中心 UI 和可用性的更改

在早期版本的映像，可以看到**逐步推出**现在显示为一个新的发货标签阶段进度栏上。 仪表板将显示在驱动程序**限制百分比**中与进度栏下方的说明文本**取消**按钮。

 ![下面逐步推出状态指示器的文本的屏幕截图。 文本介绍了标签所面向的其符合条件的填充的 100%。 此外，现可使用取消按钮。](images/gradual-rollout.png)

在您的驱动程序时**Microsoft 批准**或**逐步推出**阶段，寄送标签已锁定的任何编辑或修改。 但是，可以**取消**当时发货标签。 **取消**按钮结束整个发货标签 （过期时）。 请注意，**取消**为您的驱动程序时，可能只是功能按钮**Microsoft 批准**或**逐步推出**阶段。

## <a name="systems-included-in-the-throttled-percentages"></a>系统包含在受限制的百分比

当驱动程序正在阻止，并将分配的目标受众基线的百分比，Microsoft 将使用**整个 Windows 10 版本 1709年及更高版本零售填充**。  与 Windows 10 Windows 1703 及更早版本的设备将收到该驱动程序后限制已完成和寄送标签达到**Finalize**步骤。

## <a name="driver-throttling-assessments"></a>驱动程序限制评估

Microsoft 完成每个符合条件的驱动程序的风险评估，并将分配该驱动程序版本限制曲线。 驱动程序的风险评估针对许多因素，包括但不是局限于外部测试覆盖率和零售填充。 限制曲线或驱动程序推出，百分比紧密相关的风险评估。 此外，所有限制曲线都是很大程度上基于百分比的上的目标受众。

### <a name="rules-that-define-when-a-rollout-should-automatically-pause"></a>定义出站日志应会自动暂停的规则

如果您的驱动程序不能满足 Microsoft 质量检查，Microsoft 将暂停逐步推出过程。  Microsoft 还使用这些相同的质量检查决定时继续进行到下一步的限制级别的驱动程序。  

已暂停的驱动程序显示的限制百分比**0%** 。

功能团队或 OEM 完成调查后，Microsoft 将在暂停后继续推出过程。

>[!NOTE]
>驱动程序 Shiproom 管理员保留暂停由于其他的遥测信号而推出的权利。

### <a name="rules-that-define-when-releasestatus-should-be-set-to-complete"></a>规则，用于定义何时**ReleaseStatus**应设置为**完成**

在 30 天监视周期结束时将编辑发布传送标签。 您的合作伙伴开发人员中心仪表板上的发货标签状态会前进到**Finalize**。

## <a name="faq"></a>常见问题

### <a name="when-will-the-30-day-monitoring-period-start-and-what-should-we-expect"></a>何时开始 30 天监视内，而且我们也希望什么？

所有阻止驱动程序，请将至少 30 天内监视是否开始 1%或 100%。 发布到任何受限制状态中的零售总体时，就立即开始驱动程序的监视过程。

在此 30 天推出和监视阶段，寄送标签已锁定进行任何编辑。 可通过单击取消寄送标签**取消**寄送标签上的按钮。

如果 Microsoft 需要这 30 天时间内可能会增加**暂停**调查的驱动程序。

### <a name="is-my-driver-available-on-wu-during-gradual-rollout"></a>是我的驱动程序在逐渐推出期间 WU 上可用？

驱动程序是在 WU，但仅适用于运行 Windows 10 版本 1709年及更高版本的系统。

运行 Windows 10 版本 1703年及更早版本的系统将不能获取驱动程序，直到达到寄送标签**Finalize**。

有关**自动/严重**驱动程序，您可以使用设备管理器手动触发的驱动程序更新，无论您的驱动程序有哪些限制百分比。 这是用于运行 Windows 10 版本 1709年及更高版本的系统。 此策略，测试人员、 技术支持人员和各种 OEM 审核工具来获取驱动程序中之前**Finalize**阶段。 但是，如果**可选**-仅暂停驱动程序时，它不会通过设备管理器。

当您的驱动程序达到 100%时，该驱动程序被视为实时 WU 上对所有符合条件的系统运行 Windows 10 版本 1709年及更高版本，即使在监视阶段尚未完成。

### <a name="how-will-microsoft-notify-an-owner-if-a-driver-is-paused-or-cancelled"></a>如何将 Microsoft 通知所有者是否暂停或取消驱动程序？

暂停或取消驱动程序的通知是通过发货标签，仅。

### <a name="how-can-we-expedite-this-process-if-we-have-a-critical-business-need"></a>如何可以我们加快此过程如果我们有一项非常关键的业务需求？

提交的加急请求之前，查看所传送的标签，并检查 UI 文本消息，请参阅限制的百分比是否达到 100%。 是否在 100%，则实时 WU 上对运行 Windows 10 版本 1709年及更高版本的所有系统驱动程序。

接下来，验证和测试是否可以接收该驱动程序从设备管理器。

如果你有业务关键需求，或尝试到目标计算机中运行 Windows 10 版本 1703年或更早版本，仅提交的请求。

若要提交[支持请求](https://developer.microsoft.com/windows/hardware/support)，包括你的业务理由。 Windows 硬件工程支持页上，确保在使用你的硬件开发人员中心/合作伙伴中心登录凭据，以便我们可以正确地将你的请求链接到正确的合作伙伴帐户登录：

1. **第一个**，登录到你的硬件开发人员中心帐户，然后
2. 转到[ https://developer.microsoft.com/windows/support ](https://developer.microsoft.com/windows/support)。
3. 选择**联系我们**，**仪表板问题**，然后**硬件提交和签名 （所有 OS 版本）** 从下拉菜单。

### <a name="what-drivers-are-included-in-the-gradual-rollout"></a>逐渐推出中包括哪些驱动程序？

**所有**驱动程序将最终受到逐渐推出。