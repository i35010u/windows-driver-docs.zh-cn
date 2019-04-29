---
title: 未发生系统崩溃的情况下创建转储文件
description: 未发生系统崩溃的情况下创建转储文件
ms.assetid: 747194d0-0aac-487a-acdc-ff27721606d4
keywords:
- 转储文件，不在系统发生崩溃的情况下创建
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 211b9c107050fcfdffa4204cc8f1f75cdc120003
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375477"
---
# <a name="creating-a-dump-file-without-a-system-crash"></a>未发生系统崩溃的情况下创建转储文件


## <span id="ddk_creating_a_dump_file_without_a_system_crash_dbg"></span><span id="DDK_CREATING_A_DUMP_FILE_WITHOUT_A_SYSTEM_CRASH_DBG"></span>


如果 KD 或 WinDbg 执行内核模式调试时，它可能会导致写入而不发生崩溃的目标计算机的内核模式转储文件。

此转储文件可以是完全内存转储或小的内存转储。 控制面板设置不是与此操作相关的。

而引起系统崩溃转储文件写入已崩溃的计算机中，此转储文件将写入主计算机。

有关详细信息，请参阅[ **.dump （创建转储文件）** ](-dump--create-dump-file-.md)命令。

 

 





