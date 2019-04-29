---
title: 审核
description: 审核
ms.assetid: 0a703a27-91d6-41fc-bd46-a9486842a150
keywords:
- 安全 WDK 文件系统、 审核
- 审核 WDK 的文件系统
- 事件 WDK 文件系统
- SeAuditingFileEvents
- SeOpenObjectAuditAlarm
- 请参阅 WDK 的事件还事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e19b5884b76c873cc3c81ec3c2e1a5a4eff8bec1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393035"
---
# <a name="auditing"></a>审核


## <span id="ddk_auditing_if"></span><span id="DDK_AUDITING_IF"></span>


良好的安全设计的原则之一是不得不承认，没有安全系统没有此类的内容。 系统的开发人员必须知道人们将避开任何安全是存在。 这可以实现主动，例如，通过探测查找并攻击系统中的漏洞的安全子系统。 或者也可能是偶然的例如，无意中覆盖或删除关键数据。 无论原因如何，它是命令性构造可以检测此类漏洞的系统。

在 Windows 中的审核系统提供了一种机制用于跟踪特定的安全事件，以便可以在以后执行事后分析已损坏或被破坏系统的分析日志。 在 Windows 上的审核机制非常涉及文件系统，因为文件系统是负责维护系统数据的持久存储。 对于许多系统，安全需求低得多，并且在这些情况下，禁用审核。 文件系统必须实现的方式，它们可以解决这两个这些环境的问题。

有关审核的关键例程包括：

-   [**SeAuditingFileEvents**](https://msdn.microsoft.com/library/windows/hardware/ff554770)-此例程确定是否已在系统上启用文件审核; 这是全局策略检查，以确定是否应执行完整的审核检查。 引入了此例程来优化安全性系统操作。

-   [**SeOpenObjectAuditAlarm**](https://msdn.microsoft.com/library/windows/hardware/ff556682)-此例程执行 Windows 系统 （尝试打开某个对象的审核） 中的主审核操作。 请注意，它是尝试访问审核，则该对象不是对对象的访问是成功还是失败。

没有为审核要求。 没有任何示例文件系统 （FAT 或 CDFS，例如） IFS 部分中的 WDK 实现审核。 但是，从安全角度看，审核很重要因为它允许管理员监视系统的安全行为。

 

 




