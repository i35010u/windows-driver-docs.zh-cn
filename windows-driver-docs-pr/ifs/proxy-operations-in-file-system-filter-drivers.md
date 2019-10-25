---
title: 文件系统筛选器驱动程序中的代理操作
description: 文件系统筛选器驱动程序中的代理操作
ms.assetid: 01cc7a48-8b27-4de7-8968-8958e9512989
keywords:
- 安全 WDK 文件系统，代理操作
- 代理操作 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60c735bc1af7b9ff8732ec20e7d933fd42abb64b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841019"
---
# <a name="proxy-operations-in-file-system-filter-drivers"></a>文件系统筛选器驱动程序中的代理操作


## <span id="ddk_proxy_operations_in_file_system_filter_drivers_if"></span><span id="DDK_PROXY_OPERATIONS_IN_FILE_SYSTEM_FILTER_DRIVERS_IF"></span>


文件系统筛选器驱动程序必须经常代表原始（用户模式）调用方执行操作。 执行此操作时，文件系统筛选器驱动程序不会执行可能执行原始用户无法执行的操作的操作。 例如，假设用户尝试打开文件\_取代。 然后，筛选器驱动程序不能尝试使用[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)打开指定相同访问类型的文件，例如，即使用户没有取代该文件的权限，该操作也会在文件系统执行时成功。筛选器驱动程序。

文件系统筛选器驱动程序可能导致此类问题的方法很多。 当文件系统筛选器驱动程序在基础文件系统上执行操作时，如果不知道用户操作的结果，则可能会发生这种情况。 文件系统筛选器驱动程序必须这样识别此类情况，并确保该驱动程序已确定操作的结果，或者它具有用于从实际用户操作中的错误中恢复的机制。 例如，在请求取代该文件时，筛选器驱动程序可能需要使用[**IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)代表原始调用方打开该文件，该文件指示对该文件的安全权限，这些权限足以满足替代操作的要求。 例如，如果筛选器驱动程序使用 IO\_强制\_访问\_检查选项，则会使用当前线程的凭据进行安全检查，即使调用来自内核驱动程序也是如此。

文件系统筛选器驱动程序必须标识驱动程序在其上执行操作的实例，或执行某些用户级别操作的实例。 在这些情况下，需要确定正确操作的明确策略。

 

 




