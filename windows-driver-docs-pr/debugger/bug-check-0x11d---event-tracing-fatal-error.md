---
title: Bug 检查 0x11D EVENT_TRACING_FATAL_ERROR
description: EVENT_TRACING_FATAL_ERROR bug 检查的值为0x0000011D。 此 bug 检查指示事件跟踪子系统遇到意外错误。
keywords:
- Bug 检查 0x11D EVENT_TRACING_FATAL_ERROR
- EVENT_TRACING_FATAL_ERROR
ms.date: 12/08/2020
topic_type:
- apiref
api_name:
- EVENT_TRACING_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 16a584a4a7932bb0126b8a2832c71366a9da3ebd
ms.sourcegitcommit: 11a82f18ee7874537597792cb77f749d5ce6eee5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "96999156"
---
# <a name="bug-check-0x11d-event_tracing_fatal_error"></a>Bug 检查0x11D：事件 \_ 跟踪 \_ 严重 \_ 错误

"事件 \_ 跟踪 \_ \_ 错误 bug 检查" 的值为 "0x0000011D"。 此 bug 检查指示事件跟踪子系统遇到意外错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="resolution"></a>解决方法

在内核调试器中，使用 [**！分析-v**](-analyze.md) 命令执行初始 bug 检查分析。 参数1将列出错误检查的子类型。

0x01：无法初始化安全性。

0x02：无法初始化处理器。

0x03：内核模式注册损坏。

0x04：注销中的句柄无效。

0x05： EventWrite 调用中的数据溢出。

0x06：事件已经丢失。

0x07：跟踪缓冲区已损坏。

0x08：无法为 ETW LoggerContext 分配缓存感知断开保护。 参数2将包含记录器 Id。

0x09： ETW GuidEntry 的引用计数对于对象的当前状态是非法的。 参数2将包含一个指向 ETW_GUID_ENTRY 的指针。


## <a name="see-also"></a>另请参阅

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)
