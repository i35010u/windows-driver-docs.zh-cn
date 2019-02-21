---
title: 错误检查的 SCSI 微型端口调试
description: 错误检查的 SCSI 微型端口调试
ms.assetid: 9a517096-f708-452b-83f6-e7d4f0d41ac3
keywords:
- 调试时，bug 检查 SCSI 微型端口
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23de7d56bfd920a681e740b3808325461ed05e1c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533920"
---
# <a name="bug-checks-for-scsi-miniport-debugging"></a>错误检查的 SCSI 微型端口调试


有两个主要在调试 SCSI 微型端口驱动程序的过程中出现的 bug 检查： bug 检查 0x77 (内核\_堆栈\_页内\_错误) 和 bug 检查 0x7A (内核\_数据\_页内\_错误）。 其参数的完整详细信息，请参阅[ **Bug 检查 0x77** ](bug-check-0x77--kernel-stack-inpage-error.md)并[ **Bug 检查 0x7A**](bug-check-0x7a--kernel-data-inpage-error.md)。

每个这些 bug 检查指示发生分页错误。 有三个主要原因这些 bug 检查：

-   由于特定设备上的超时或没有活动的适配器上重置的完整总线

-   所选内容超时

-   控制器错误

若要确定失败的确切原因，请首先使用[ **！ scsikd.classext** ](-scsikd-classext.md)扩展，它显示最近失败的请求，包括 SRB 状态、 SCSI 状态有关的信息和请求的检测数据。

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

在上一示例中，操作码 0x2A 表示一个写入操作，并 0x28 指示读取的操作。 在示例中的 SCSI 状态是 02，指示检查条件。 探测代码提供错误详细信息。

与往常一样，微型端口驱动程序开发人员负责将从其硬件到 SRB 状态代码的错误代码相关联。 通常情况下，超时是 SRB 0x0A，选择超时值的代码与相关联。 SRB 0x0e 程序通常与完整总线重置，但它还可与控制器错误相关联。

 

 





