---
title: 管理内存节
description: 管理内存节
ms.assetid: 620ba31d-596f-493a-b97f-65a27d50cc9a
keywords:
- 内存部分 WDK 内核
- 部分对象 WDK 内核
- 视图 WDK 内存部分
- 映射部分视图
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66078fa565a02b943ff4214cc356fef276504288
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386012"
---
# <a name="managing-memory-sections"></a>管理内存节





驱动程序可以通过调用创建的部分对象[ **ZwCreateSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatesection)，其中返回的句柄的部分对象。 使用*FileHandle*参数来指定备份文件，或**NULL**如果该节不提供文件支持。 可以使用打开的部分对象的其他句柄[ **ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)。

若要使属于在当前进程的地址空间中访问的部分对象的数据，必须映射部分中的视图。 驱动程序可以将映射节的视图到当前进程的地址空间使用[ **ZwMapViewOfSection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwmapviewofsection)例程。 *SectionOffset*参数指定的部分视图的开始处的字节偏移量和*ViewSize*指定要映射的字节数。

*保护*参数指定在视图上允许的操作。 指定页\_只读视图中，页的 READONLY\_READWRITE 读/写视图和页面\_WRITECOPY 写入时复制视图。

没有物理内存分配图，直到访问虚拟内存范围。 内存范围在首次访问会导致页错误;然后，系统会分配页来保存该内存位置。 如果该节被文件备份，系统将读取对应于相应页面，并将其复制到内存中的文件的内容。 （请注意未使用的部分对象和视图执行用于簿记目的使用一些分页和非分页池）。

驱动程序不能再使用视图后，它取消映射，它通过调用[ **ZwUnmapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwunmapviewofsection)。 驱动程序不再使用的部分对象后，它将关闭与部分句柄[ **ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)。 请注意，映射视图并不将任何其他视图映射后，它是安全地立即调用**ZwClose**部分句柄; 视图 （和部分对象） 继续存在，直到该视图是未映射。 这是建议的做法，因为它减少了无法关闭句柄的驱动程序的风险。

 

 




