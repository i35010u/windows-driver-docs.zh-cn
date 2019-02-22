---
title: 有没有缓冲区的基于 IRP 的 I/O 操作
description: 有没有缓冲区的基于 IRP 的 I/O 操作
ms.assetid: f1666a01-11f1-47e4-9e8d-bbfb5f85893a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dad78cd3bb76206c53275068fd091303716949f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540541"
---
# <a name="irp-based-io-operations-that-have-no-buffers"></a>有没有缓冲区的基于 IRP 的 I/O 操作


## <span id="ddk_irp_based_io_operations_that_have_no_buffers_if"></span><span id="DDK_IRP_BASED_IO_OPERATIONS_THAT_HAVE_NO_BUFFERS_IF"></span>


以下基于 IRP 的 I/O 操作具有任何缓冲区，并因此没有任何缓冲的方法：

-   IRP\_MJ\_CREATE\_MAILSLOT

-   IRP\_MJ\_CREATE\_NAMED\_PIPE

-   IRP\_MJ\_锁\_控件

 

 




