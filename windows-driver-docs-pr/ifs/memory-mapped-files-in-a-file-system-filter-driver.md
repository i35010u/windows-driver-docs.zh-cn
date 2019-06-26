---
title: 文件系统筛选器驱动程序中的内存映射文件
description: 文件系统筛选器驱动程序中的内存映射文件
ms.assetid: 0915167a-f8ac-4222-bece-76d7fc8a3823
keywords:
- 安全 WDK 文件系统、 内存映射文件
- 内存映射文件 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cef17d2e49f4664adab20de77d0291a833298f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375966"
---
# <a name="memory-mapped-files-in-a-file-system-filter-driver"></a>文件系统筛选器驱动程序中的内存映射文件


## <span id="ddk_memory_mapped_files_in_a_file_system_filter_driver_if"></span><span id="DDK_MEMORY_MAPPED_FILES_IN_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


文件系统筛选器驱动程序必须确定的这一事实文件可以进行访问，通过虚拟内存映射文件，而不是通过读取和写入路径。 监视文件中的更改的文件系统筛选器驱动程序将丢失对此类文件的更改。 一般情况下想要使用内存映射 I/O 处理的文件系统筛选器驱动程序必须筛选分页 I/O。 许多方法解决此问题将在 Windows 文件系统开发人员列表中讨论[(NTFSD)](http://www.osronline.com/cf.cfm^PageURL=showlists.cfm^list=NTFSD.htm%253f.htm)由 OSR 承载的新闻组。

 

 




