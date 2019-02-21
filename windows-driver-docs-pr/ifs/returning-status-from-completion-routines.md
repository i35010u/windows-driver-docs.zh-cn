---
title: 从完成例程返回状态
description: 从完成例程返回状态
ms.assetid: fb12720b-10fe-43ab-ade7-c1b09d00d922
keywords:
- IRP 完成例程 WDK 文件系统，返回状态
- 状态值 WDK 文件系统
- 成功状态的值 WDK 文件系统
- 返回状态 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9716f55e9f35c1a51adc3549aa210095583c8f30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544946"
---
# <a name="returning-status-from-completion-routines"></a>从完成例程返回状态


## <span id="ddk_returning_status_from_completion_routines_if"></span><span id="DDK_RETURNING_STATUS_FROM_COMPLETION_ROUTINES_IF"></span>


文件系统筛选器驱动程序完成例程通常情况下返回以下两个 NTSTATUS 值之一调用方：

-   状态\_成功

-   状态\_更多\_处理\_必需

状态\_成功指示驱动程序完成处理 IRP，若要继续完成处理 IRP，I/O 管理器。

状态\_更多\_处理\_必需暂停 I/O 管理器完成处理 IRP。

如果返回任何其他 NTSTATUS 值，则 I/O 管理器将其重置到状态\_成功。

有关返回状态详细信息\_更多\_处理\_必需的请参阅[完成例程的约束](constraints-on-completion-routines.md)。

 

 




