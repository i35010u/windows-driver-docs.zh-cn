---
title: Bug 检查 0x149 REFS_FILE_SYSTEM
description: REFS_FILE_SYSTEM bug 检查的值为0x00000149。 这表明发生了文件系统错误。
ms.assetid: 899E89E7-46CD-4143-B1DC-7959F01643CF
keywords:
- Bug 检查 0x149 REFS_FILE_SYSTEM
- REFS_FILE_SYSTEM
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- REFS_FILE_SYSTEM
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f6e36636600ee91523922e92dfedc6791c9aaf3e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534842"
---
# <a name="bug-check-0x149-refs_file_system"></a>Bug 检查0x149： REFS \_ 文件 \_ 系统


REFS \_ 文件 \_ 系统 bug 检查的值为0x00000149。 这表明发生了文件系统错误。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="refs_file_system-parameters"></a>REFS \_ 文件 \_ 系统参数


| 参数 | 说明                          |
|-----------|--------------------------------------|
| 1         | \_\_内嵌\_\_                         |
| 2         | ExceptionRecord                      |
| 3         | ContextRecord                        |
| 4         | ExceptionRecord- &gt; ExceptionAddress |

 

| 参数 | 说明 |
|-----------|-------------|
| 1         | Message     |
| 2         | 保留    |
| 3         | 保留    |
| 4         | 保留    |

 

<a name="resolution"></a>解决方法
----------

如果在堆栈上看到 RefsExceptionFilter，则第二个和第三个参数是异常记录和上下文记录。 在第二个参数上执行[**.exr**](-exr--display-exception-record-.md)以查看异常信息，然后在第三个参数和[**kb**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)上执行[**.cxr**](-cxr--display-context-record-.md) ，以获取更有意义的堆栈跟踪。

 

 




