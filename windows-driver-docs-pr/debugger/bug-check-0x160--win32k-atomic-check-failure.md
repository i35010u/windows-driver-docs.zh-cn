---
title: Bug 检查 0x160 WIN32K_ATOMIC_CHECK_FAILURE
description: WIN32K_ATOMIC_CHECK_FAILURE bug 检查具有 0x00000160 值。 这表示 Win32k 函数已违反 ATOMICCHECK。
ms.assetid: 81EEC1ED-367A-477D-B008-2295C7D7D1B4
keywords:
- Bug 检查 0x160 WIN32K_ATOMIC_CHECK_FAILURE
- WIN32K_ATOMIC_CHECK_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- WIN32K_ATOMIC_CHECK_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: cce623e1949e7ca30d2f727d5f22c6ddd108e552
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564923"
---
# <a name="bug-check-0x160-win32katomiccheckfailure"></a>Bug 检查 0x160：WIN32K\_原子\_检查\_失败


WIN32K\_原子\_检查\_故障错误检查的值为 0x00000160。 这表示 Win32k 函数已违反 ATOMICCHECK。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="win32katomiccheckfailure-parameters"></a>WIN32K\_原子\_检查\_失败参数


| 参数 | 描述                                                             |
|-----------|-------------------------------------------------------------------------|
| 1         | 函数内以原子操作的当前堆栈上的计数 |
| 2         | 保留                                                                |
| 3         | 保留                                                                |
| 4         | 保留                                                                |

 

 

 




