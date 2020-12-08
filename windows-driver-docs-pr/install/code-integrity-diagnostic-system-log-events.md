---
title: 代码完整性诊断系统日志事件
description: 代码完整性诊断系统日志事件
keywords:
- 代码完整性 WDK 驱动程序签名
- 事件 WDK 驱动程序签名
- 状态信息 WDK 驱动程序签名
- 详细诊断事件 WDK 驱动程序签名
- 审核事件 WDK 驱动程序签名
- 记录 WDK 驱动程序签名
- 诊断日志事件 WDK 代码完整性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bd27db8d97c1f8654fc9cf4941c6ccd018f0fbb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782995"
---
# <a name="code-integrity-diagnostic-system-log-events"></a>代码完整性诊断系统日志事件


Windows Vista 和更高版本的 Windows 的代码完整性组件强制要求对内核模式驱动程序进行签名才能加载。 Windows Vista 和更高版本的 Windows 始终会生成代码完整性操作事件，并根据需要生成其他系统审核事件和详细诊断事件，以提供有关驱动程序签名状态的信息，如下所示：

-   代码完整性操作日志包含警告事件，这些事件指示无法加载内核模式驱动程序，因为无法验证驱动程序签名。 签名验证可能会失败，原因如下：
    -   管理员预安装了未签名的驱动程序，但代码完整性随后阻止加载未签名的驱动程序。
    -   驱动程序已签名，但签名无效，因为驱动程序文件已更改。
    -   从坏磁盘扇区读取驱动程序的文件时，系统磁盘设备可能出现设备错误。
-   如果启用系统审核策略，则代码完整性将生成与操作警告事件对应的系统审核日志事件，这些事件表明驱动程序文件的签名验证失败。 默认情况下不启用系统审核策略。

-   如果启用了代码完整性的详细日志记录，则代码完整性将记录分析和调试事件，这些事件提供有关在加载内核模式驱动程序文件之前发生的成功验证检查的信息。 默认情况下，不启用代码完整性的详细日志记录。

可以使用事件查看器查看代码完整性事件，如 [查看代码完整性事件](viewing-code-integrity-events.md)中所述。 有关这些事件日志消息的详细信息，请参阅 [代码完整性事件日志消息](code-integrity-event-log-messages.md)。

有关如何启用系统审核日志和详细日志记录的详细信息，请参阅 [启用系统事件审核日志](enabling-the-system-event-audit-log.md)。

 

 





