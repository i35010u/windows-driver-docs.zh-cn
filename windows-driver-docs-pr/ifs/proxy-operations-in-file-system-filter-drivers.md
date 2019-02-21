---
title: 在文件系统筛选器驱动程序中的代理操作
description: 在文件系统筛选器驱动程序中的代理操作
ms.assetid: 01cc7a48-8b27-4de7-8968-8958e9512989
keywords:
- 安全 WDK 文件系统，代理操作
- 代理操作 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f2e14c7ba51fd00ddd8a95ea761b3d2fa8ea747
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523657"
---
# <a name="proxy-operations-in-file-system-filter-drivers"></a>在文件系统筛选器驱动程序中的代理操作


## <span id="ddk_proxy_operations_in_file_system_filter_drivers_if"></span><span id="DDK_PROXY_OPERATIONS_IN_FILE_SYSTEM_FILTER_DRIVERS_IF"></span>


文件系统筛选器驱动程序必须频繁地执行代表原始 （用户模式） 调用方的操作。 这样做时，它是命令性文件系统筛选器驱动程序不执行的操作，可能需要原始用户不可能的操作。 例如，假设用户尝试打开文件进行文件\_SUPERSEDE。 筛选器驱动程序不能再尝试打开文件指定相同类型的访问[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)，例如，因为即使用户没有权限来取代该文件，文件系统筛选器驱动程序执行时，操作会成功。

在其中的文件系统筛选器驱动程序可能会引入此类问题的方法有很多。 它们可的随时文件系统筛选器驱动程序不知道用户的操作结果的情况下执行基础文件系统上的操作发生。 因此，文件系统筛选器驱动程序必须识别这种情况下，并确保它要么已确定该操作的结果，或者它具有用于从实际用户操作中的错误中恢复的机制。 例如，对于取代该文件的请求，筛选器驱动程序可能需要打开代表原始调用方使用的文件[ **IoCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff548418) ，该值指示对该文件的安全权限的将足以满足 supersede 操作。 如果筛选器驱动程序已使用 IO\_FORCE\_访问\_检查选项，例如，安全检查操作即告完成，在当前线程的凭据即使在调用是从内核驱动程序。

它是必需的文件系统筛选器驱动程序来标识的实例驱动程序正在其中执行操作代表的或为，一些用户级操作。 在这些情况下，如何确保操作正确的清除策略需要进行标识。

 

 




