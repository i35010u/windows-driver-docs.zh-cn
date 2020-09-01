---
title: 使用 IRP 优先级提示
description: 使用 IRP 优先级提示
ms.assetid: c34afff2-32f2-451b-ab16-ff048d5c3204
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e48e444ff8f97bbcc7c5905b2feb84ff19ec8174
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192459"
---
# <a name="using-irp-priority-hints"></a>使用 IRP 优先级提示


*Irp 优先级提示*是与 IRP 关联的[**IO \_ 优先级 \_ 提示**](/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_priority_hint)值。 IRP 优先级提示提供了一个简单的提示机制，用于指示 Irp 相对重要性。 选择处理 IRP 的顺序时，驱动程序可以使用 IRP 的优先级提示。 IRP 优先级提示在 Windows Vista 及更高版本的操作系统上可用。

有关 IRP 优先级提示的详细信息，请参阅 [Windows Vista 中的 I/o 优先顺序](https://go.microsoft.com/fwlink/p/?linkid=67877) 白皮书。

 

