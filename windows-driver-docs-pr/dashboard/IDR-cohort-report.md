---
title: 队列失败报告
description: 描述取消后系统提供的队列失败报告
ms.topic: article
ms.date: 10/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: c035b65c2897cdee3ce664da86e88912e34d1991
ms.sourcegitcommit: 068a9875851a278935078ba7f1ab65a3bb37235c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2020
ms.locfileid: "92100648"
---
# <a name="cohort-failure-report"></a>队列失败报告

从 2020 年 6 月 15 日开始，驱动程序服务开始[通过目标队列来评估驱动程序质量](https://docs.microsoft.com/windows-hardware/drivers/dashboard/overview-of-microsoft-driver-measure-dictionary#evaluating-by-targeting-cohort)。 为了改进此过程，从 2020 年 10 月 30 日开始，如果驱动程序由于队列失败而被取消，你将开始收到一份详细说明[失败](https://docs.microsoft.com/windows-hardware/drivers/dashboard/overview-of-microsoft-driver-measure-dictionary#evaluating-by-targeting-cohort)细节的新报告。

## <a name="location-of-the-report"></a>报告位置

驱动程序完成外部测试后，系统会创建一个 bug 并将其分配给你，该 bug 中包括决策快照（外部测试完成时度量值状态的报告）[下图中的 report.html]。 如果在发布监视过程中驱动程序由于队列失败而被取消，我们将利用该 bug 来包括新的队列失败报告。 它将以该 bug 附件的形式添加到 RejectedDriverFlightReport Zip 文件中。 在该 Zip 文件中，文件名将为 Cohort_Failure_Report.pdf。

![附加了 RejectDriverFlightReport.zip 文件的 Bug 附件的屏幕截图，该文件包含新的 Cohort_Failure_Report.pdf](images/IDRReportBug.png) 图 1：附加了 RejectedDriverFlightReport.zip 文件的 Bug 附件的屏幕截图，该文件包含新的 Cohort_Failure_Report.pdf

## <a name="how-to-read-the-report"></a>如何阅读报告

此报告包含 3 个部分，分别为“标题”、“摘要”和“详细信息”，如下所述  。

### <a name="title-section-describes-the-driver"></a>标题部分：描述驱动程序

本部分包括提交者的公司名称、报告的生成日期、发货标签编号、驱动程序名称和驱动程序版本。

![“标题”部分的屏幕截图，其中包括提交者的公司名称、报告日期、发货标签、驱动程序名称和驱动程序版本](images/IDRReportTitle.png)图 2：“标题”部分的屏幕截图，其中包括提交者的公司名称、报告日期、发货标签、驱动程序名称和驱动程序版本

### <a name="summary-section-provides-a-summary-of-the-action-you-will-need-to-take"></a>摘要部分：提供需要执行的操作的摘要

本部分包含有关完成的分析类型以及解决该问题可采取的措施的基本信息。

![“摘要”部分的屏幕截图，其中包含报告摘要以及解决该问题可采取的措施](images/IDRReportSummary.png)图 3：“摘要”部分的屏幕截图，其中包含报告摘要以及解决该问题可采取的措施

### <a name="details-section-provides-details-about-the-failures-that-were-found"></a>详细信息部分：提供有关所发现的失败的详细信息

本部分包括有关所发现的失败的详细信息。 对于发现的每个失败队列，都将重复本部分内容。 

本部分首先列出在其中发现失败的目标队列（硬件 ID、CHID 和 OS 版本）， 其次列出针对该目标队列的失败的度量值，包括：

- 度量值 ID（在度量值字典和外部测试版报告中查找）。
- 度量值名称
- 报告时的度量值结果
- 通过标准
- 度量值状态
- 该队列中已采用驱动程序并用于计算度量值的计算机数。

![“详细信息”部分的屏幕截图，其中包括每个失败的目标队列和每个队列的失败度量值详细信息](images/IDRReportDetails.png)图 4：“详细信息”部分的屏幕截图，其中包括每个失败的目标队列和每个队列的失败度量值详细信息
