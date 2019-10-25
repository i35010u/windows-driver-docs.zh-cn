---
title: 审核
description: 审核
ms.assetid: 0a703a27-91d6-41fc-bd46-a9486842a150
keywords:
- 安全 WDK 文件系统，审核
- 审核 WDK 文件系统
- 事件 WDK 文件系统
- SeAuditingFileEvents
- SeOpenObjectAuditAlarm
- 事件 WDK，另请参阅事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37525f66392af208c7e7495693a2a4b841a6bd53
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841485"
---
# <a name="auditing"></a>审核


## <span id="ddk_auditing_if"></span><span id="DDK_AUDITING_IF"></span>


良好的安全设计原则之一是承认这种情况并不是安全系统。 系统的开发人员必须知道，人们会绕过任何安全性。 例如，可以通过探查安全子系统来查找并利用系统内的洞来实现此目的。 否则，可能会意外覆盖或删除关键数据。 无论原因是什么，都必须构建一个可检测此类违规的系统。

Windows 中的审核系统提供了一种机制，用于跟踪特定的安全事件，以便以后可以对日志进行分析，以便对受损或被破坏的系统执行事后分析。 Windows 它紧密上的审核机制涉及文件系统，因为文件系统负责维护系统数据的持久存储。 在许多系统中，安全需求要低得多，在这种情况下，将禁用审核。 文件系统的实现方式必须能够解决这两种环境中的问题。

审核的关键例程包括：

-   [**SeAuditingFileEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seauditingfileevents)-此例程确定是否已在系统上启用文件审核;这是一种全局策略检查，用于确定是否应执行完整审核检查。 引入此例程是为了优化安全系统操作。

-   [**SeOpenObjectAuditAlarm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seopenobjectauditalarm)-此例程在 Windows 系统中执行主要审核操作（审核尝试打开对象）。 请注意，尝试访问已审核的对象，而不是对对象的访问是成功还是失败。

无需审核。 WDK 的 IFS 部分中没有任何示例文件系统（例如 FAT 或 CDFS）实现审核。 但是，从安全角度来看，审核非常重要，因为它允许管理员监视系统的安全行为。

 

 




