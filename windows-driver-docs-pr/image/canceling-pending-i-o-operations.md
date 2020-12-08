---
title: 取消挂起的 I/O 操作
description: 取消挂起的 I/O 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5bb5e23e42251d64d0e9246bdc1d3992b14f678
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840985"
---
# <a name="canceling-pending-io-operations"></a>取消挂起的 I/O 操作





WIA 应用程序可使用 Microsoft Windows SDK 文档)  (中所述的 **IWiaItemExtras：： CancelPendingIO** 方法来取消 WIA 微型驱动程序当前可能正在处理的任何挂起的 i/o 操作。 **IWiaItemExtras：： CancelPendingIO** 方法使用 WIA 事件 CANCEL IO 事件调用 [**IWiaMiniDrv：:d rvnotifypnpevent**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法 \_ \_ \_ 。 WIA 微型驱动程序应取消所有当前 i/o 操作并返回到空闲状态。

可随时调用 **IWiaItemExtras：： CancelPendingIO** 方法。 建议所有内核模式读取或写入操作都使用 [重叠 i/o](../kernel/handling-overlapped-i-o-operations.md)。 这样就可以立即取消。 遇到意外延迟或看似挂起的 WIA 应用程序可以调用 **IWiaItemExtras：： CancelPendingIO** 方法，以尝试将控制权返回给最终用户。

 

