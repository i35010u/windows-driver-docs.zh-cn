---
title: Bug 检查 0x1CB INVALID_SILO_DETACH
description: INVALID_SILO_DETACH bug 检查具有 0x000001CB 值。 它指示某个线程未能在退出之前从接收器分离。
keywords:
- Bug 检查 0x1CB INVALID_SILO_DETACH
- INVALID_SILO_DETACH
ms.date: 02/21/2019
topic_type:
- apiref
api_name:
- INVALID_SILO_DETACH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e228b443f8214e878b2158db80d3239cf2d761db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361659"
---
# <a name="bug-check-0x1cb-invalidsilodetach"></a>Bug 检查 0x1CB：无效\_接收器\_分离

无效\_接收器\_分离错误检查的值为 0x000001CB。 它指示某个线程未能在退出之前从接收器分离。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

 

## <a name="invalidsilodetach-parameters"></a>无效\_接收器\_分离参数

|参数|描述|
|-------- |---------- |
|1| 对附加线程的指针。 |
|2| 以前附加接收器。 |
|3| 到线程的进程的指针。 |
|4| 保留。 |


## <a name="cause"></a>原因
-----
线程退出之前从接收器分离失败。 



## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

