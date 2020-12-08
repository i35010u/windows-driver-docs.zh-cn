---
title: 文件系统筛选器驱动程序中的模拟
description: 文件系统筛选器驱动程序中的模拟
keywords:
- 安全 WDK 文件系统，模拟
- 模拟 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 495174544330b83167fe8146d8bfd4fdd5a17c24
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816779"
---
# <a name="impersonation-in-a-file-system-filter-driver"></a>文件系统筛选器驱动程序中的模拟


## <span id="ddk_impersonation_in_a_file_system_filter_driver_if"></span><span id="DDK_IMPERSONATION_IN_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


文件系统筛选器驱动程序可能尝试使用的另一个操作是模拟。 尽管模拟是一种非常强大的技术，用于代表其他线程处理安全，但它也要求代表任何组件使用适当的处理方法。 对于文件系统筛选器驱动程序，必须使用模拟来确定需要完成的操作。 然后，确保不应使用模拟执行由文件系统筛选器驱动程序执行的其他操作。 模拟的风险通常是调用方的特权少于发出调用的驱动程序的特权。 因此，如果使用模拟进行调用，则它可能会失败，而不会发生模拟的情况。

任何创建新句柄的操作都需要模拟，因为句柄表示对对象的引用，并且是执行安全检查的点。 例如，使用 [**ZwCreateSection**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatesection)、 [**ZwCreateEvent**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-zwcreateevent)和 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)打开文件或其他对象 (时需要模拟，例如) 。 在这些调用中，调用它们的筛选器驱动程序必须确保要传递的参数是有效的，因为其他操作系统操作将假定源自内核模式的调用将具有有效的参数。 因此，筛选器驱动程序不能安全地将用户缓冲区地址传递给这些函数中的任何一个，即使在模拟时也是如此。

如果是 [**ZwCreateFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)，则需要将相应的 i/o 管理器调用 [**IoCreateFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatefile)用于模拟，因为它允许筛选器驱动程序指定 IO \_ 强制 \_ 访问 \_ 检查。 缺少此选项，i/o 管理器将不会强制执行适当的用户级别访问检查。

 

