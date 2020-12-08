---
title: 用于 SCSI 微型端口调试的 Bug 检查
description: 用于 SCSI 微型端口调试的 Bug 检查
keywords:
- SCSI 微型端口调试，bug 检查
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6da46243061447492f7669191c56f2c4a447ade
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821635"
---
# <a name="bug-checks-for-scsi-miniport-debugging"></a>用于 SCSI 微型端口调试的 Bug 检查


在调试 SCSI 微型端口驱动程序的过程中，主要有两个 bug 检查： bug 检查 0x77 (内核 \_ 堆栈 \_ INPAGE \_ 错误) 和 bug 检查 0x7A (内核 \_ 数据 \_ INPAGE \_ 错误) 。 有关参数的完整详细信息，请参阅 [**Bug 检查 0x77**](bug-check-0x77--kernel-stack-inpage-error.md) 和 [**bug 检查 0x7A**](bug-check-0x7a--kernel-data-inpage-error.md)。

其中每个 bug 检查都表明出现了分页错误。 这些错误检查的主要原因有三个：

-   由于特定设备上的超时或适配器上无活动而发生了完全总线重置

-   选择超时

-   控制器错误

若要确定失败的确切原因，请首先使用 [**！ scsikd. classext**](-scsikd-classext.md) 扩展，其中显示了有关最近失败的请求的信息，包括请求的 SRB 状态、SCSI 状态和感知数据。

```dbgcmd
kd> !scsikd.classext 816e96b0
Storage class device 816e96b0 with extension at 816e9768

Classpnp Internal Information at 817b4008

    Failed requests:

           Srb    Scsi
    Opcode Status Status Sense Code  Sector   Time  Stamp
    ------ ------ ------ ---------- -------- ------------
      2a     0a     02    03 0c 00  0000abcd 23:01:07.453  Retried
      28     0a     02    03 04 00  0000abcd 23:01:07.984  Retried

dt classpnp!_CLASS_PRIVATE_FDO_DATA 817b4008 -

...
```

在上面的示例中，opcode 0x2A 指明了写入操作，0x28 指示读取操作。 示例中的 SCSI 状态为02，这表示检查条件。 理解代码提供更多错误信息。

与往常一样，小型小型驱动程序开发人员负责将其硬件的错误代码关联到 SRB 状态代码。 通常，超时值与 SRB 0x0A （选择超时的代码）相关联。 SRB 0x0e 通常与完全总线重置相关联，但也可能与控制器错误相关联。

 

 





