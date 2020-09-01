---
title: 检查 PendingReturned 标志
description: 检查 PendingReturned 标志
ms.assetid: cdcdffb0-4210-4bf0-984e-b0c3234df129
keywords:
- IRP 完成例程 WDK 文件系统，PendingReturned 标志
- PendingReturned 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43c6a67abb3980b44ab2768612953a7da80f0003
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065342"
---
# <a name="checking-the-pendingreturned-flag"></a>检查 PendingReturned 标志


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


如果完成例程未发出事件信号，则必须检查 **Irp- &gt; PendingReturned** 标志。 如果设置了此标志，则完成例程必须通过调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)将 IRP 标记为挂起。

 

