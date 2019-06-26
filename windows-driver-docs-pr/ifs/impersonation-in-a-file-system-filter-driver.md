---
title: 文件系统筛选器驱动程序中的模拟
description: 文件系统筛选器驱动程序中的模拟
ms.assetid: ee56cd54-01ac-46ad-8ee4-e76131b058f3
keywords:
- 安全 WDK 文件系统模拟
- 模拟 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 13eaab1da6e87e96f0641c2917eaa72a247279d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375703"
---
# <a name="impersonation-in-a-file-system-filter-driver"></a>文件系统筛选器驱动程序中的模拟


## <span id="ddk_impersonation_in_a_file_system_filter_driver_if"></span><span id="DDK_IMPERSONATION_IN_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


文件系统筛选器驱动程序可能会尝试使用另一个操作是模拟。 模拟时用于处理代表其他线程的安全很强大的技术，它还用于代表任何组件需要适当小心。 文件系统筛选器驱动程序，务必要确定需要执行的操作使用模拟。 然后，务必确保不应完成其他操作执行的文件系统筛选器驱动程序使用模拟。 调用方具有较少的权限比驱动程序进行调用，通常是使用模拟的风险。 因此，如果使用模拟进行调用，它可能会失败，而不使用模拟，则会成功。

模拟是所需的任何操作都创建新的句柄，因为该句柄表示对对象的引用，并且是在其中执行安全检查的点。 例如，模拟时是必需的打开的文件或其他对象 (使用[ **ZwCreateSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatesection)， [ **ZwCreateEvent**](https://msdn.microsoft.com/library/windows/hardware/ff566423)，和[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)，例如)。 在这些调用，调用这些方法筛选器驱动程序必须确保所传递的参数是有效，因为其他操作系统操作将假定调用源自于内核模式下将包含有效参数。 因此，筛选器驱动程序不能安全地传递用户缓冲区地址到任何这些函数，即使模拟。

情况下[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)，没有相应的 I/O 管理器调用[ **IoCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatefile)，应与一起使用模拟因为它允许筛选器驱动程序，以指定 IO\_FORCE\_访问\_检查。 缺少此选项时，I/O 管理器不会强制适当的用户级别访问权限检查。

 

 




