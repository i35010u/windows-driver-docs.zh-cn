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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556132"
---
# <a name="checking-the-pendingreturned-flag"></a>检查 PendingReturned 标志


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


如果完成例程不会向事件发送信号，则必须检查**Irp‑&gt;PendingReturned**标志。 如果设置此标志，完成例程必须通过调用标记挂起的 IRP [ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)。

 

 




