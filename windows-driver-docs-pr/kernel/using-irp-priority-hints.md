---
title: 使用 IRP 优先级提示
description: 使用 IRP 优先级提示
ms.assetid: c34afff2-32f2-451b-ab16-ff048d5c3204
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f26eb5e1e9e65365a2d1ec74b5e8e271e186412a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838350"
---
# <a name="using-irp-priority-hints"></a>使用 IRP 优先级提示


*Irp 优先级提示*是与 IRP 关联[ **\_提示值的 IO\_优先级**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_io_priority_hint)。 IRP 优先级提示提供了一个简单的提示机制，用于指示 Irp 相对重要性。 选择处理 IRP 的顺序时，驱动程序可以使用 IRP 的优先级提示。 IRP 优先级提示在 Windows Vista 及更高版本的操作系统上可用。

有关 IRP 优先级提示的详细信息，请参阅[Windows Vista 中的 I/o 优先顺序](https://go.microsoft.com/fwlink/p/?linkid=67877)白皮书。

 

 




