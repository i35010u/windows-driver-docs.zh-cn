---
title: 检查 PendingReturned 标志
description: 检查 PendingReturned 标志
keywords:
- IRP 完成例程 WDK 文件系统，PendingReturned 标志
- PendingReturned 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e8f2b8e13016ce0793e52dde4340689083a275f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810045"
---
# <a name="checking-the-pendingreturned-flag"></a>检查 PendingReturned 标志


## <span id="ddk_checking_the_pendingreturned_flag_if"></span><span id="DDK_CHECKING_THE_PENDINGRETURNED_FLAG_IF"></span>


如果完成例程未发出事件信号，则必须检查 **Irp- &gt; PendingReturned** 标志。 如果设置了此标志，则完成例程必须通过调用 [**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)将 IRP 标记为挂起。

 

