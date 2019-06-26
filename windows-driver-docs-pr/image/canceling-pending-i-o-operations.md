---
title: 取消挂起的 I/O 操作
description: 取消挂起的 I/O 操作
ms.assetid: 58383836-5922-4499-a73d-d17d26dd2f76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96726fe9430f8065d07e06c9fd7bf03c2b8f477f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366723"
---
# <a name="canceling-pending-io-operations"></a>取消挂起的 I/O 操作





WIA 应用程序可以使用**IWiaItemExtras::CancelPendingIO** （Microsoft Windows SDK 文档中所述） 的方法来取消任何挂起的 WIA 微型驱动程序可能当前正在处理的 I/O 操作。 **IWiaItemExtras::CancelPendingIO**方法调用[ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)方法使用 WIA\_事件\_取消\_IO 事件。 WIA 微型驱动程序应取消所有当前的 I/O 操作并返回到空闲状态。

**IWiaItemExtras::CancelPendingIO**可以在任何时候调用方法。 建议所有内核模式下读取或写入操作使用[重叠 I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-overlapped-i-o-operations)。 这允许发生立即取消。 出现意外的延迟，或显示为挂起的 WIA 应用程序可以调用**IWiaItemExtras::CancelPendingIO**方法尝试将控制权返回给最终用户。

 

 




