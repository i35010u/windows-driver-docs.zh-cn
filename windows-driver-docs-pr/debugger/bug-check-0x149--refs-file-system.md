---
title: Bug 检查 0x149 REFS_FILE_SYSTEM
description: REFS_FILE_SYSTEM bug 检查的值为0x00000149。 这表明发生了文件系统错误。
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
ms.openlocfilehash: b95fd555a1c45d28c2884945e22b521027c6cc07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805769"
---
# <a name="bug-check-0x149-refs_file_system"></a>Bug 检查0x149： REFS \_ 文件 \_ 系统


REFS \_ 文件 \_ 系统 bug 检查的值为0x00000149。 这表明发生了文件系统错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="refs_file_system-parameters"></a>REFS \_ 文件 \_ 系统参数


| 参数 | 描述                          |
|-----------|--------------------------------------|
| 1         | \_\_内嵌\_\_                         |
| 2         | ExceptionRecord                      |
| 3         | ContextRecord                        |
| 4         | ExceptionRecord- &gt; ExceptionAddress |

 

| 参数 | 描述 |
|-----------|-------------|
| 1         | 消息     |
| 2         | 预留    |
| 3         | 预留    |
| 4         | 预留    |

 

<a name="resolution"></a>解决方法
----------

如果在堆栈上看到 RefsExceptionFilter，则第二个和第三个参数是异常记录和上下文记录。 在第二个参数上执行 [**.exr**](-exr--display-exception-record-.md)以查看异常信息，然后在第三个参数和 [**kb**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)上执行 [**.cxr**](-cxr--display-context-record-.md) ，以获取更有意义的堆栈跟踪。

 

 




