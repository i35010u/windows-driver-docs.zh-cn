---
title: C28714
description: 语义不同的整数类型之间的警告 C28714 转换。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28714
ms.openlocfilehash: f18d089c6a19a53a10e7c1fc6b87bf6852629688
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837329"
---
# <a name="c28714"></a>C28714


警告 C28714：语义不同的整数类型之间的强制转换

此警告指示将 **NTSTATUS** 值显式转换为布尔类型。 这可能会产生意外的结果。 例如，在作为布尔值进行测试时， **NTSTATUS** 的典型成功值（ **状态 \_ 成功**）为 **false** 。

在大多数情况下，应该使用 **NT \_ SUCCESS** 宏来测试 **NTSTATUS** 的值。 如果返回的状态值既不是警告也不是错误代码，则此宏返回 **true** 。 如果函数返回布尔值以指示失败/成功，则它应显式返回合适的布尔类型，而不是依赖于将 **NTSTATUS** 强制转换为布尔类型。

此外，有时程序可能会尝试重复使用布尔本地变量来存储 **NTSTATUS** 值。 这种做法通常是容易出错的; (和可能更高效) 使用单独的 **NTSTATUS** 变量，这是更安全的做法。

 

 





