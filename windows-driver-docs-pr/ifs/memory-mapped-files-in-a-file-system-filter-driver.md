---
title: 文件系统筛选器驱动程序中的内存映射文件
description: 文件系统筛选器驱动程序中的内存映射文件
ms.assetid: 0915167a-f8ac-4222-bece-76d7fc8a3823
keywords:
- 安全 WDK 文件系统，内存映射文件
- 内存映射文件 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 066e20156d90aa25289971dbf7a84acb21a9c3c8
ms.sourcegitcommit: 67efcd26f7be8f50c92b141ccd14c9c68f4412d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88902536"
---
# <a name="memory-mapped-files-in-a-file-system-filter-driver"></a>文件系统筛选器驱动程序中的内存映射文件

文件系统筛选器驱动程序必须 cognizant，因为可以通过文件的虚拟内存映射来访问文件，而不是通过读取和写入路径访问文件。 文件系统筛选器驱动程序监视文件中的更改将丢失对此类文件的更改。 通常，要处理内存映射 i/o 的文件系统筛选器驱动程序必须筛选分页 i/o。 Minifilters 托管的 [Windows 文件系统和开发人员](https://community.osr.com/) 新闻组中讨论了用于处理此情况的许多技术。
