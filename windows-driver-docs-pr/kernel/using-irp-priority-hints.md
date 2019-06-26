---
title: 使用 IRP 优先级提示
description: 使用 IRP 优先级提示
ms.assetid: c34afff2-32f2-451b-ab16-ff048d5c3204
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b95d6bc15b496e46042d3211c37ae43b001de5d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383288"
---
# <a name="using-irp-priority-hints"></a>使用 IRP 优先级提示


*IRP 优先级提示*是[ **IO\_优先级\_提示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_io_priority_hint)与 IRP 相关联的值。 IRP 优先级提示提供一个简单的提示机制，以指示 Irp 的相对重要性。 选择处理 IRP 的顺序时驱动程序可以使用 IRP 优先级提示。 IRP 优先级提示是在 Windows Vista 和更高版本操作系统上可用。

有关 IRP 优先级提示的详细信息，请参阅[Windows Vista 中的 I/O 优先级](https://go.microsoft.com/fwlink/p/?linkid=67877)白皮书。

 

 




