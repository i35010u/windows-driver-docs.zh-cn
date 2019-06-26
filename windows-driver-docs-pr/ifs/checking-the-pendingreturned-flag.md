---
title: 检查 PendingReturned 标志
description: 检查 PendingReturned 标志
ms.assetid: cdcdffb0-4210-4bf0-984e-b0c3234df129
keywords:
- IRP 完成例程 WDK 文件系统，PendingReturned 标志
- PendingReturned 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be4e5e06114cfaaa1a87edc50c19b80bc65e948b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379007"
---
# <a name="checking-the-pendingreturned-flag"></a>检查 PendingReturned 标志


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


如果完成例程不会向事件发送信号，则必须检查**Irp‑&gt;PendingReturned**标志。 如果设置此标志，完成例程必须通过调用标记挂起的 IRP [ **IoMarkIrpPending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)。

 

 




