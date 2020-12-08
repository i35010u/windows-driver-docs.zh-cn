---
title: 文件系统筛选器驱动程序中的代理操作
description: 文件系统筛选器驱动程序中的代理操作
keywords:
- 安全 WDK 文件系统，代理操作
- 代理操作 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32ab15aa81bb95ff6de81e020265410eb959af3b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838603"
---
# <a name="proxy-operations-in-file-system-filter-drivers"></a>文件系统筛选器驱动程序中的代理操作


## <span id="ddk_proxy_operations_in_file_system_filter_drivers_if"></span><span id="DDK_PROXY_OPERATIONS_IN_FILE_SYSTEM_FILTER_DRIVERS_IF"></span>


文件系统筛选器驱动程序必须经常代表原始 (用户模式) 调用方执行操作。 执行此操作时，文件系统筛选器驱动程序不会执行可能执行原始用户无法执行的操作的操作。 例如，假设用户尝试打开文件以进行文件 \_ 取代。 然后，筛选器驱动程序不能尝试使用 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)打开指定相同访问类型的文件，例如，即使用户没有取代该文件的权限，当文件系统筛选器驱动程序执行该操作时，操作也会成功。

文件系统筛选器驱动程序可能导致此类问题的方法很多。 当文件系统筛选器驱动程序在基础文件系统上执行操作时，如果不知道用户操作的结果，则可能会发生这种情况。 文件系统筛选器驱动程序必须这样识别此类情况，并确保该驱动程序已确定操作的结果，或者它具有用于从实际用户操作中的错误中恢复的机制。 例如，在请求取代该文件时，筛选器驱动程序可能需要使用 [**IoCreateFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile) 代表原始调用方打开该文件，该文件指示对该文件的安全权限，这些权限足以满足替代操作的要求。 例如，如果筛选器驱动程序要使用 IO \_ 强制 \_ 访问 \_ 检查选项，则会使用当前线程的凭据执行安全检查，即使该调用来自内核驱动程序。

文件系统筛选器驱动程序必须标识驱动程序在其上执行操作的实例，或执行某些用户级别操作的实例。 在这些情况下，需要确定正确操作的明确策略。

 

