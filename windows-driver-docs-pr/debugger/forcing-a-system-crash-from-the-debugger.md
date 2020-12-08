---
title: 通过调试器强制系统崩溃
description: 通过调试器强制系统崩溃
keywords:
- 系统崩溃，导致调试器
- bug 检查，由调试器引起
- 从调试器强制系统崩溃
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 117c7b796fe87d1d57c9fe4e18a0df241d134aa2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838191"
---
# <a name="forcing-a-system-crash-from-the-debugger"></a>通过调试器强制系统崩溃


## <span id="ddk_forcing_a_system_crash_from_the_debugger_dbg"></span><span id="DDK_FORCING_A_SYSTEM_CRASH_FROM_THE_DEBUGGER_DBG"></span>


如果 KD 或 WinDbg 正在执行内核模式调试，则可能会强制系统崩溃。 这是通过在命令提示符下输入 " [**崩溃 (强制系统崩溃)**](-crash--force-system-crash-.md) 命令来完成的。  (如果目标计算机不能立即崩溃，请遵循 [**g (中转)**](g--go-.md) 命令。 ) 

发出此命令时，系统将调用 **KeBugCheck** 并发出 [**bug 检查 0xE2**](bug-check-0xe2--manually-initiated-crash.md) (手动 \_ 启动 \_ 崩溃) 。 除非已禁用故障转储，否则将在此时写入故障转储文件。

在写入故障转储文件后，将会提醒主机计算机上的内核调试器，并可使用该调试程序主动调试崩溃的目标。

 

 





