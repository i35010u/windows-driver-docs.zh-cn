---
title: 取消挂起的 I/O 操作
description: 取消挂起的 I/O 操作
ms.assetid: 58383836-5922-4499-a73d-d17d26dd2f76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6857b872230b60366110bcb87e5b3c91aceefdad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840881"
---
# <a name="canceling-pending-io-operations"></a>取消挂起的 I/O 操作





WIA 应用程序可以使用**IWiaItemExtras：： CancelPendingIO**方法（如 Microsoft Windows SDK 文档中所述）来取消 WIA 微型驱动程序当前可能正在处理的任何挂起的 i/o 操作。 **IWiaItemExtras：： CancelPendingIO**方法使用 WIA\_事件调用[**IWiaMiniDrv：:d RVNOTIFYPNPEVENT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法\_CANCEL\_IO 事件。 WIA 微型驱动程序应取消所有当前 i/o 操作并返回到空闲状态。

可随时调用**IWiaItemExtras：： CancelPendingIO**方法。 建议所有内核模式读取或写入操作都使用[重叠 i/o](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-overlapped-i-o-operations)。 这样就可以立即取消。 遇到意外延迟或看似挂起的 WIA 应用程序可以调用**IWiaItemExtras：： CancelPendingIO**方法，以尝试将控制权返回给最终用户。

 

 




