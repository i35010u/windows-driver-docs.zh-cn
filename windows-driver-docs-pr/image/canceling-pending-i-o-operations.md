---
title: 取消挂起的 I/O 操作
description: 取消挂起的 I/O 操作
ms.assetid: 58383836-5922-4499-a73d-d17d26dd2f76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b88634e045d0d7a11cacb6c878922476dba1c764
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192729"
---
# <a name="canceling-pending-io-operations"></a>取消挂起的 I/O 操作





WIA 应用程序可使用 Microsoft Windows SDK 文档)  (中所述的 **IWiaItemExtras：： CancelPendingIO** 方法来取消 WIA 微型驱动程序当前可能正在处理的任何挂起的 i/o 操作。 **IWiaItemExtras：： CancelPendingIO**方法使用 WIA 事件 CANCEL IO 事件调用[**IWiaMiniDrv：:d rvnotifypnpevent**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法 \_ \_ \_ 。 WIA 微型驱动程序应取消所有当前 i/o 操作并返回到空闲状态。

可随时调用 **IWiaItemExtras：： CancelPendingIO** 方法。 建议所有内核模式读取或写入操作都使用 [重叠 i/o](../kernel/handling-overlapped-i-o-operations.md)。 这样就可以立即取消。 遇到意外延迟或看似挂起的 WIA 应用程序可以调用 **IWiaItemExtras：： CancelPendingIO** 方法，以尝试将控制权返回给最终用户。

 

