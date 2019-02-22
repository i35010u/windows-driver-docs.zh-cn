---
title: 取消挂起的 I/O 操作
description: 取消挂起的 I/O 操作
ms.assetid: 58383836-5922-4499-a73d-d17d26dd2f76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 982d86395097ba9faae9e96c7df076ef38de9fd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545297"
---
# <a name="canceling-pending-io-operations"></a>取消挂起的 I/O 操作





WIA 应用程序可以使用**IWiaItemExtras::CancelPendingIO** （Microsoft Windows SDK 文档中所述） 的方法来取消任何挂起的 WIA 微型驱动程序可能当前正在处理的 I/O 操作。 **IWiaItemExtras::CancelPendingIO**方法调用[ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)方法使用 WIA\_事件\_取消\_IO 事件。 WIA 微型驱动程序应取消所有当前的 I/O 操作并返回到空闲状态。

**IWiaItemExtras::CancelPendingIO**可以在任何时候调用方法。 建议所有内核模式下读取或写入操作使用[重叠 I/O](https://msdn.microsoft.com/library/windows/hardware/ff546911)。 这允许发生立即取消。 出现意外的延迟，或显示为挂起的 WIA 应用程序可以调用**IWiaItemExtras::CancelPendingIO**方法尝试将控制权返回给最终用户。

 

 




