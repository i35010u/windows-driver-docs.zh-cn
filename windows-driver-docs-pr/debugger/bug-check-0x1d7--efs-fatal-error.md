---
title: Bug 检查 0x1D7 EFS_FATAL_ERROR
description: EFS_FATAL_ERROR bug 检查的值为0x000001D7。 它表示发生了 EFS 错误情况，因此无法在不丢失数据或损坏数据的情况下进行处理。
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
ms.openlocfilehash: 5d63f37da94efab687b99ef079540c05ad1a1649
ms.sourcegitcommit: e0bec5347825e04fb3b2309d04156b01a83fa593
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2020
ms.locfileid: "88090118"
---
# <a name="bug-check-0x1d7-efs_fatal_error"></a>Bug 检查0x1D7： EFS \_ 严重 \_ 错误

EFS \_ \_ 错误 bug 检查的值为0x000001D7。 它表示发生了 EFS 错误情况，因此无法在不丢失数据或损坏数据的情况下进行处理。


> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

 

## <a name="efs_fatal_error-parameters"></a>EFS \_ \_ 错误参数

|参数|说明|
|-------- |---------- |
|1| Bug 检查子类： **01** -预卸载失败。|
|2| 操作的 NTSTATUS 返回代码。|
|3| 失败时的当前 IRP。|
|4| 出现故障时的文件加密上下文。|

## <a name="cause"></a>原因
-----

发生了 EFS 错误情况，因此无法在不丢失数据或损坏数据的情况下进行处理。

## <a name="resolution"></a>解决方法
-----

[！分析](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

检查参数 2 NTSTATUS 字段，尝试并确定未返回 NT_SUCCESS 的原因。 这是调用加密预卸载的文件系统所需且唯一允许的值。

使用调试器[！](-irp.md)用于调查参数3是否可能存在冲突的 irp 代码或其他问题的 IRP 命令。



## <a name="see-also"></a>另请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

