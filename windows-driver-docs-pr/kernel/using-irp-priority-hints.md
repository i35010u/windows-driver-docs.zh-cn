---
title: 使用 IRP 优先级提示
description: 使用 IRP 优先级提示
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7ffe35918e730ae86ba82c1716f4ffe038b52d5b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817155"
---
# <a name="using-irp-priority-hints"></a>使用 IRP 优先级提示


*Irp 优先级提示* 是与 IRP 关联的 [**IO \_ 优先级 \_ 提示**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_priority_hint)值。 IRP 优先级提示提供了一个简单的提示机制，用于指示 Irp 相对重要性。 选择处理 IRP 的顺序时，驱动程序可以使用 IRP 的优先级提示。 IRP 优先级提示在 Windows Vista 及更高版本的操作系统上可用。

有关 IRP 优先级提示的详细信息，请参阅 [Windows Vista 中的 I/o 优先顺序](https://go.microsoft.com/fwlink/p/?linkid=67877) 白皮书。

 

