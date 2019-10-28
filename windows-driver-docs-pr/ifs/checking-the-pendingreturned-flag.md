---
title: 检查 PendingReturned 标志
description: 检查 PendingReturned 标志
ms.assetid: cdcdffb0-4210-4bf0-984e-b0c3234df129
keywords:
- IRP 完成例程 WDK 文件系统，PendingReturned 标志
- PendingReturned 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ae8538bd1951ab94d81a7079c1a134f51deba97
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841477"
---
# <a name="checking-the-pendingreturned-flag"></a>检查 PendingReturned 标志


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


如果完成例程未发出事件信号，则必须检查**Irp&gt;PendingReturned**标志。 如果设置了此标志，则完成例程必须通过调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)将 IRP 标记为挂起。

 

 




