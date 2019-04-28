---
title: 检查 PendingReturned 标志
description: 检查 PendingReturned 标志
ms.assetid: cdcdffb0-4210-4bf0-984e-b0c3234df129
keywords:
- IRP 完成例程 WDK 文件系统，PendingReturned 标志
- PendingReturned 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 040aae998f8fe74a6abe88c35cec8563bcc7e10f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327907"
---
# <a name="checking-the-pendingreturned-flag"></a>检查 PendingReturned 标志


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


如果完成例程不会向事件发送信号，则必须检查**Irp‑&gt;PendingReturned**标志。 如果设置此标志，完成例程必须通过调用标记挂起的 IRP [ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)。

 

 




