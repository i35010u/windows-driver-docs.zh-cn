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
ms.openlocfilehash: ba35c541a9fe91a3dbad463b6256f266787e8d80
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358094"
---
# <a name="bug-check-0x160-win32katomiccheckfailure"></a>Bug 检查 0x160：WIN32K\_原子\_检查\_失败


WIN32K\_原子\_检查\_故障错误检查的值为 0x00000160。 这表示 Win32k 函数已违反 ATOMICCHECK。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="win32katomiccheckfailure-parameters"></a>WIN32K\_原子\_检查\_失败参数


| 参数 | 描述                                                             |
|-----------|-------------------------------------------------------------------------|
| 1         | 函数内以原子操作的当前堆栈上的计数 |
| 2         | 保留                                                                |
| 3         | 保留                                                                |
| 4         | 保留                                                                |

 

 

 




