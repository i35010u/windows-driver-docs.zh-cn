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
ms.openlocfilehash: 8c7f56e3a0cce42c01aa5f0082df06da52d851f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367756"
---
# <a name="bug-check-0x160-win32katomiccheckfailure"></a>Bug 检查 0x160：WIN32K\_原子\_检查\_失败


WIN32K\_原子\_检查\_故障错误检查的值为 0x00000160。 这表示 Win32k 函数已违反 ATOMICCHECK。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="win32katomiccheckfailure-parameters"></a>WIN32K\_原子\_检查\_失败参数


| 参数 | 描述                                                             |
|-----------|-------------------------------------------------------------------------|
| 1         | 函数内以原子操作的当前堆栈上的计数 |
| 2         | 保留                                                                |
| 3         | 保留                                                                |
| 4         | 保留                                                                |

 

 

 




