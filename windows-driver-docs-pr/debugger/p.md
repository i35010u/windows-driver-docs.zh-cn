---
title: P （Windows 调试器词汇表）
description: 术语表页-P
Robots: noindex, nofollow
ms.assetid: 4cfad26c-d8c0-4f80-aa54-b9cadbc84df3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2137a5b6327e425eaa10b2eb2b092ade573d5dce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520011"
---
# <a name="p"></a>P


<span id="page_table"></span><span id="PAGE_TABLE"></span>**页表**  
将虚拟内存地址映射到物理内存地址的特定于进程的表。

<span id="page_table_entry__pte_"></span><span id="PAGE_TABLE_ENTRY__PTE_"></span>**页表项 (PTE)**  
页表中的项。

<span id="paged_pool"></span><span id="PAGED_POOL"></span>**页面缓冲的池**  
部分系统内存进行分页到磁盘。

请注意，此术语不只是指实际实际上已调出至磁盘的内存-它包括任何允许使用操作系统的内存页。

<span id="paging"></span><span id="PAGING"></span>**paging**  
在其中内存管理器将传输页从内存到磁盘变满物理内存时虚拟内存操作。 一个*页面错误*线程访问不在内存中的页面时发生。

<span id="parent_symbol"></span><span id="PARENT_SYMBOL"></span>**父符号**  
一个*符号*这就是包含在其他符号，例如，结构中包含其成员。

另请参阅*子符号*。

有关详细信息，请参阅[作用域和符号组](scopes-and-symbol-groups.md)。

<span id="primary_client"></span><span id="PRIMARY_CLIENT"></span>**主客户端**  
已加入当前调试会话的客户端对象

有关详细信息，请参阅[客户端对象](client-objects.md)。

<span id="process_server"></span><span id="PROCESS_SERVER"></span>**进程服务器**  
充当代理，侦听来自智能客户端的连接并根据这些远程客户端的请求执行内存、 处理器、 或 Windows 操作调试器引擎的实例。

另请参阅*调试服务器*。

有关详细信息，请参阅[的进程服务器 （用户模式）](process-servers--user-mode-.md)和进程服务器和智能客户端。

<span id="processor_breakpoint"></span><span id="PROCESSOR_BREAKPOINT"></span>**处理器断点**  
由处理器实现一个断点。 调试器引擎指示要插入此断点的目标的处理器。

另请参阅软件断点。 另请参阅*软件断点*。

有关详细信息，请参阅[使用断点](using-breakpoints.md)。

 

 





