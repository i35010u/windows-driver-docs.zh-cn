---
title: 代码完整性诊断系统日志事件
description: 代码完整性诊断系统日志事件
ms.assetid: 4aa8db3e-033c-4f38-a813-623518e36485
keywords:
- 代码完整性 WDK 驱动程序签名
- 事件 WDK 驱动程序签名
- 状态信息 WDK 驱动程序签名
- 详细的诊断事件 WDK 驱动程序签名
- 审核事件 WDK 驱动程序签名
- 记录 WDK 驱动程序签名
- 诊断日志事件 WDK 代码完整性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9f1f19c3272fa47845cd41e7e64f3e02a729747
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361174"
---
# <a name="code-integrity-diagnostic-system-log-events"></a>代码完整性诊断系统日志事件


代码完整性组件的 Windows Vista 和更高版本的 Windows 强制要求的内核模式驱动程序进行了签名，以便加载。 Windows Vista 和更高版本的 Windows 始终生成代码完整性操作事件，并根据需要将生成额外的系统审核事件和提供的驱动程序签名，按如下所示的状态信息的详细诊断事件：

-   代码完整性运行日志包括指示无法加载，因为无法验证驱动程序签名的内核模式驱动程序的警告事件。 签名验证可能会出于以下原因失败：
    -   管理员预安装未签名的驱动程序，但代码完整性随后阻止加载未签名的驱动程序。
    -   该驱动程序进行签名，但签名无效，因为驱动程序文件已被更改。
    -   从损坏的磁盘扇区的驱动程序读取该文件时，系统磁盘设备可能有设备错误。
-   如果启用了系统审核策略，代码完整性生成对应的警告事件，指示该签名验证失败的驱动程序文件的操作的系统审核日志事件。 默认情况下不启用系统审核策略。

-   如果启用详细日志记录的代码完整性，代码完整性日志分析和调试提供加载内核模式驱动程序文件之前发生的成功验证检查有关的信息的事件。 默认情况下未启用代码完整性的详细日志记录。

您可以使用事件查看器查看代码完整性事件，如中所述[查看代码完整性事件](viewing-code-integrity-events.md)。 有关这些事件日志消息的详细信息，请参阅[代码完整性事件日志消息](code-integrity-event-log-messages.md)。

有关如何启用系统审核日志和详细日志记录的详细信息，请参阅[启用系统事件审核日志](enabling-the-system-event-audit-log.md)。

 

 





