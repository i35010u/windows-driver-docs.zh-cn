---
title: Bug 检查 0x1D7 EFS_FATAL_ERROR
description: EFS_FATAL_ERROR bug 检查具有 0x000001D7 值。 它指示，以便不能解决数据丢失或数据损坏而发生了 EFS 错误条件。
keywords:
- Bug 检查 0x1D7 EFS_FATAL_ERROR
- EFS_FATAL_ERROR
ms.date: 01/22/2019
topic_type:
- apiref
api_name:
- EFS_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 58c1882671aadd3a4eff171e792219067d048eab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361603"
---
# <a name="bug-check-0x1d7-efsfatalerror"></a>Bug 检查 0x1D7：EFS\_致命错误\_错误

EFS\_致命错误\_错误 bug 检查的值为 0x000001D7。 它指示，以便不能解决数据丢失或数据损坏而发生了 EFS 错误条件。


> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

 

## <a name="efsfatalerror-parameters"></a>EFS\_致命错误\_错误参数

|参数|描述|
|-------- |---------- |
|1| Bug 检查子类：**01** -预卸载失败。|
|2| NTSTATUS 返回操作的代码。|
|3| 在失败时的当前 IRP。|
|4| 在失败时的文件加密上下文。|

## <a name="cause"></a>原因
-----

这样，不能解决数据丢失或数据损坏而发生了 EFS 错误情况。

## <a name="resolution"></a>分辨率
-----

[！ 分析](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

检查参数 2 NTSTATUS 字段，并尝试确定未返回 NT_SUCCESS 的原因。 这是预期的和仅允许调用加密预卸载的文件系统的值。

使用调试器[！IRP](-irp.md)命令以调查参数 3 的可能冲突的 IRP 代码或其他问题。



## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

