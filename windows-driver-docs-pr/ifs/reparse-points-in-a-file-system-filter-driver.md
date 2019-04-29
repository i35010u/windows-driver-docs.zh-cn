---
title: 文件系统筛选器驱动程序中的重新分析点
description: 文件系统筛选器驱动程序中的重新分析点
ms.assetid: 6aae70d9-c934-4759-bb26-728b0ac025d1
keywords:
- 安全 WDK 文件系统，重新分析点
- 重新分析点 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9dccec8fc849213a3a07b6f4a4346852e0de52d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377943"
---
# <a name="reparse-points-in-a-file-system-filter-driver"></a>文件系统筛选器驱动程序中的重新分析点


## <span id="ddk_reparse_points_in_a_file_system_filter_driver_if"></span><span id="DDK_REPARSE_POINTS_IN_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


进程重新分析点的筛选器驱动程序必须了解应用程序可能会创建无效的重分析点的风险。 若要确保严格的安全，句柄重新分析点，必须确保数据内容的重新分析点本身的驱动程序是可验证，无论是通过安全的校验和、 加密的内容或其他机制，以确保无效的重新分析点无法创建无特权的应用程序。 例如，筛选器驱动程序可能要求其重新分析点是使用应用程序 （或本地安全机构，例如） 之间共享的密码进行加密，驱动程序，以确保数据内容的重新分析点就有效。

否则，它是可能的恶意应用程序可以创建具有无效的重分析点信息的重分析点。 在这种情况下，文件系统筛选器驱动程序必须准备好处理无效的重分析点数据，包括自引用数据 （创建引用循环可能导致溢出时，某种类型的数据）、 数据溢出问题和无效数据内容。

 

 




