---
title: P （Windows 调试器术语表）
description: 词汇表页-P
ms.assetid: 4cfad26c-d8c0-4f80-aa54-b9cadbc84df3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcde64d30d167868f498fa484cb509dae5c70999
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387028"
---
# <a name="p"></a>P


<span id="page_table"></span><span id="PAGE_TABLE"></span>**页表**  
特定于进程的表，该表将虚拟内存地址映射到物理内存地址。

<span id="page_table_entry__pte_"></span><span id="PAGE_TABLE_ENTRY__PTE_"></span>**页表项（PTE）**  
页表中的项。

<span id="paged_pool"></span><span id="PAGED_POOL"></span>**页面缓冲池**  
可以分页到磁盘的系统内存的一部分。

请注意，此术语并不只是指实际已实际分页到磁盘的内存，它包括允许操作系统页面的任何内存。

<span id="paging"></span><span id="PAGING"></span>**分页**  
一种虚拟内存操作，在此操作中，内存管理器会在物理内存变满时将页从内存传输到磁盘。 当线程访问不在内存中的页时，将发生*页错误*。

<span id="parent_symbol"></span><span id="PARENT_SYMBOL"></span>**父符号**  
一个包含在其他符号中的*符号*，例如，结构包含其成员。

另请参阅*子符号*。

有关详细信息，请参阅[作用域和符号组](scopes-and-symbol-groups.md)。

<span id="primary_client"></span><span id="PRIMARY_CLIENT"></span>**主客户端**  
已联接当前调试会话的客户端对象

有关详细信息，请参阅[客户端对象](client-objects.md)。

<span id="process_server"></span><span id="PROCESS_SERVER"></span>**进程服务器**  
作为代理的调试器引擎实例，侦听来自智能客户端的连接，并执行这些远程客户端请求的内存、处理器或 Windows 操作。

另请参阅*调试服务器*。

有关详细信息，请参阅[进程服务器（用户模式）](process-servers--user-mode-.md)和进程服务器和智能客户端。

<span id="processor_breakpoint"></span><span id="PROCESSOR_BREAKPOINT"></span>**处理器断点**  
处理器实现的断点。 调试器引擎指示目标处理器插入此断点。

另请参阅软件断点。 另请参阅*软件断点*。

有关详细信息，请参阅[使用断点](using-breakpoints.md)。

 

 





