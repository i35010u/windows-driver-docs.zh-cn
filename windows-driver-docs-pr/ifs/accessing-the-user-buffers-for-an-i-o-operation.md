---
title: 对于 I/O 操作中访问用户缓冲区
description: 对于 I/O 操作中访问用户缓冲区
ms.assetid: 0f4334bf-eec9-4667-af02-537e3357d872
keywords:
- 缓冲区 WDK 文件系统微筛选器
- FLT_PARAMETERS
- 内存描述符列出 WDK 文件系统微筛选器
- MDLs WDK 文件系统
- I/O WDK 的文件系统
- 基于 IRP 的 I/O 操作 WDK 文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4be47d8817a10fea2477b0d51c37f9d8d80712d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546857"
---
# <a name="accessing-the-user-buffers-for-an-io-operation"></a>对于 I/O 操作中访问用户缓冲区


## <span id="ddk_accessing_the_user_buffers_for_an_io_operation_if"></span><span id="DDK_ACCESSING_THE_USER_BUFFERS_FOR_AN_IO_OPERATION_IF"></span>


[ **FLT\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff544673)结构的 I/O 操作中包含该操作，包括缓冲区地址的特定于操作的参数和内存描述符的列表 (MDL)在操作中使用任何缓冲区。

对于基于 IRP 的 I/O 操作，可以通过使用指定的缓冲区的操作：

-   仅 MDL （尤其是对于分页 I/O）

-   仅缓冲区地址

-   缓冲区地址和 MDL

对于快速 I/O 操作，指定用户空间缓冲区地址。 拥有缓冲区的快速 I/O 操作始终使用既不缓冲，也不直接 I/O，并因此永远不会有 MDL 参数。

以下主题提供了指导原则微筛选器驱动程序中的基于 IRP 和快速 I/O 操作处理的缓冲区地址和 MDLs [ **preoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551109)和[ **postoperation 回调例程**](https://msdn.microsoft.com/library/windows/hardware/ff551107):

[访问 Preoperation 回调例程中的用户缓冲区](accessing-user-buffers-in-a-preoperation-callback-routine.md)

[访问 Postoperation 回调例程中的用户缓冲区](accessing-user-buffers-in-a-postoperation-callback-routine.md)

 

 




