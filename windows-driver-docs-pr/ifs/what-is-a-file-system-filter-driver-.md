---
title: 什么是文件系统筛选器驱动程序
description: 什么是文件系统筛选器驱动程序
ms.assetid: 4bff8ad6-624a-429d-b9ec-3f96c3c7c99d
keywords:
- 筛选器驱动程序 WDK 文件系统，有关文件系统筛选器驱动程序
- 文件系统筛选器驱动程序 WDK，有关文件系统筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77ae4d5f87ec5f709eb58673e1030a31a1223e76
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566973"
---
# <a name="what-is-a-file-system-filter-driver"></a>什么是文件系统筛选器驱动程序？


## <span id="ddk_what_is_a__file_system_filter_driver_if"></span><span id="DDK_WHAT_IS_A__FILE_SYSTEM_FILTER_DRIVER_IF"></span>


一个*文件系统筛选器驱动程序*是可选的驱动程序，将值添加到或修改文件系统的行为。 文件系统筛选器驱动程序是作为 Windows 高级管理人员的一部分运行的内核模式组件。

文件系统筛选器驱动程序可以筛选一个或多个文件系统或文件系统卷的 I/O 操作。 根据该驱动程序的性质*筛选器*可能意味着*日志*，*观察*，*修改*，或甚至*阻止*. 文件系统筛选器驱动程序的典型应用程序包括防病毒实用程序、 加密程序和分层存储管理系统。

 

 




