---
title: 从完成例程返回状态
description: 从完成例程返回状态
keywords:
- IRP 完成例程 WDK 文件系统，返回状态
- status 值 WDK 文件系统
- 成功状态值 WDK 文件系统
- 返回状态 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23feb23e6d88d97e549fc9f039877758c8281f8b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783938"
---
# <a name="returning-status-from-completion-routines"></a>从完成例程返回状态


## <span id="ddk_returning_status_from_completion_routines_if"></span><span id="DDK_RETURNING_STATUS_FROM_COMPLETION_ROUTINES_IF"></span>


文件系统筛选器驱动程序完成例程通常会将以下两个 NTSTATUS 值中的一个值返回给调用方：

-   状态 \_ 成功

-   状态 \_ 需要更多 \_ 处理 \_

状态 \_ 成功表示驱动程序已通过 irp 完成，并允许 I/o 管理器继续完成 irp 的处理。

状态 \_ \_ 所需的更多处理会 \_ 阻止 i/o 管理器在 IRP 上完成处理。

如果返回任何其他 NTSTATUS 值，i/o 管理器会将其重置为状态 " \_ 成功"。

有关返回状态 \_ 更多所需的处理的详细信息 \_ \_ ，请参阅 [完成例程的约束](constraints-on-completion-routines.md)。

 

 




