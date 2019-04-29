---
title: 通过调试器强制系统崩溃
description: 通过调试器强制系统崩溃
ms.assetid: 7d7d9b07-00a3-4f87-8eb9-01b3f2fa312f
keywords:
- 在系统发生崩溃，导致从调试器
- 错误检查，从而导致从调试器
- 从调试器强制系统崩溃
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6cb6b4a90323a247a652f8f6b4c1567206f68a7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371654"
---
# <a name="forcing-a-system-crash-from-the-debugger"></a>通过调试器强制系统崩溃


## <span id="ddk_forcing_a_system_crash_from_the_debugger_dbg"></span><span id="DDK_FORCING_A_SYSTEM_CRASH_FROM_THE_DEBUGGER_DBG"></span>


如果 KD 或 WinDbg 执行内核模式调试时，它可以强制发生系统崩溃。 这是通过输入[ **.crash （强制系统崩溃）** ](-crash--force-system-crash-.md)命令在命令提示符处。 (如果目标计算机不会立即崩溃，请执行此操作与[ **g （转向）** ](g--go-.md)命令。)

当发出此命令时，系统将调用**KeBugCheck**和问题[ **bug 检查 0xE2** ](bug-check-0xe2--manually-initiated-crash.md) (手动\_启动\_崩溃)。 除非已禁用故障转储，此时写入崩溃转储文件。

写入崩溃转储文件后，主机计算机上的内核调试器将发出警报，并可用于主动调试崩溃的目标。

 

 





