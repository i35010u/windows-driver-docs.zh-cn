---
title: 未发生系统崩溃的情况下创建转储文件
description: 未发生系统崩溃的情况下创建转储文件
keywords:
- 转储文件，在没有系统崩溃的情况下创建
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 584e049606827f74c2340f1f0fb7508806f774b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836879"
---
# <a name="creating-a-dump-file-without-a-system-crash"></a>未发生系统崩溃的情况下创建转储文件


## <span id="ddk_creating_a_dump_file_without_a_system_crash_dbg"></span><span id="DDK_CREATING_A_DUMP_FILE_WITHOUT_A_SYSTEM_CRASH_DBG"></span>


如果 KD 或 WinDbg 正在执行内核模式调试，则可能会导致写入内核模式转储文件而不会损坏目标计算机。

此转储文件可以是完整内存转储，也可以是小内存转储。 控制面板设置与此操作无关。

由于系统崩溃导致的转储文件被写入到已崩溃的计算机，因此此转储文件将写入主机。

有关详细信息，请参阅 [**dump (创建转储文件)**](-dump--create-dump-file-.md) 命令。

 

 





