---
title: 修改参数
description: 修改参数
ms.assetid: 01accd7f-7aa6-4f83-b8b4-81c04cd48dac
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，修改参数
- 交换缓冲区 WDK 文件系统微筛选器
- 缓冲区 WDK 文件系统微筛选器
- 内存描述符列出 WDK 文件系统微筛选器
- MDLs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47f4b3175b27ccc6a882bdd1a4548ec032cbaaa7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384277"
---
# <a name="modifying-parameters"></a>修改参数


微筛选器驱动程序可以修改与 I/O 操作，如目标实例、 目标文件对象和特定于操作的参数包括缓冲区地址和内存描述符列表 (MDL) 地址关联的某些参数。 微筛选器驱动程序通常修改的 I/O 请求其 preoperation 回调中的参数。 如果微筛选器驱动程序修改参数，它必须调用[ **FltSetCallbackDataDirty** ](https://msdn.microsoft.com/library/windows/hardware/ff544383)通知参数已更改的筛选器管理器。 它还应从其 preoperation 回调传递，以便它们可供其 postoperation 回调的上下文中记录的更改。

微筛选器驱动程序可以更改操作的 I/O 状态时完成其 preoperation 回调或未通过其 postoperation 回调中的操作中的操作 (例如，更改状态\_于错误状态成功)。 不需要调用[ **FltSetCallbackDataDirty** ](https://msdn.microsoft.com/library/windows/hardware/ff544383)这种情况下。

有关修改参数的详细信息，请参阅[修改为一个 I/O 操作的参数，](modifying-the-parameters-for-an-i-o-operation.md)。

可以通过"交换缓冲区"的 I/O 请求的缓冲区字段替换为自己的缓冲区微筛选器驱动程序。 这样的微筛选器驱动程序负责保持 I/O 请求的 MDL 和缓冲区字段的同步。筛选器管理器设置 FLTFL\_回调\_数据\_系统\_缓冲区\_标志中[ **FLT\_回调\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff544620)结构，以指示缓冲区是否是系统缓冲区; 如果存在，微筛选器驱动程序必须分配从非分页缓冲池的替换缓冲区，并且将 MDL 字段设置为**NULL**。 否则为可以从分页或非分页缓冲池分配缓冲区，微筛选器驱动程序必须始终创建并设置 MDL。 (从分页或非分页缓冲池可以在快速 I/O 操作的情况下分配新缓冲区，并且应该 MDL **NULL**。)微筛选器驱动程序必须释放缓冲区或 MDL 替换，并且必须释放任何 MDL 成功插入该实体到回调数据结构 （筛选器管理器将代表微筛选器驱动程序免费 MDL）。 到 MDL 或缓冲区更改后，微筛选器驱动程序必须调用[ **FltSetCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff544383)。

微筛选器驱动程序必须注册在其中它交换缓冲区的任何操作的 postoperation 回调。 在此回调例程中，微筛选器驱动程序必须释放它分配任何缓冲区。 除非微筛选器驱动程序调用筛选器管理器将释放 MDL [ **FltRetainSwappedBufferMdlAddress**](https://msdn.microsoft.com/library/windows/hardware/ff544352); 在这种情况下，微筛选器驱动程序负责释放 MDL。 微筛选器驱动程序可以调用[ **FltGetSwappedBufferMdlAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff543161)若要获取其 preoperation 回调中设置缓冲区的 MDL。

如果它已在其中交换缓冲区操作期间微筛选器驱动程序被卸载，该操作不能"排出";相反，将取消该操作，筛选器管理器等待操作完成，然后卸载微筛选器驱动程序。

请参阅 SwapBuffers 示例有关的交换缓冲区的微筛选器驱动程序示例。

### <a name="span-idfiltermanagerroutinesformodifyingparametersspanspan-idfiltermanagerroutinesformodifyingparametersspanspan-idfiltermanagerroutinesformodifyingparametersspanfilter-manager-routines-for-modifying-parameters"></a><span id="Filter_Manager_Routines_for_Modifying_Parameters"></span><span id="filter_manager_routines_for_modifying_parameters"></span><span id="FILTER_MANAGER_ROUTINES_FOR_MODIFYING_PARAMETERS"></span>修改参数筛选管理器例程

筛选器管理器提供以下支持例程用于修改 preoperation 和 postoperation 回调例程中的 I/O 操作参数：

[**FltClearCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff541853)

[**FltIsCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff543311)

[**FltSetCallbackDataDirty**](https://msdn.microsoft.com/library/windows/hardware/ff544383)

下面的例程提供交换缓冲区的支持：

[**FltGetSwappedBufferMdlAddress**](https://msdn.microsoft.com/library/windows/hardware/ff543161)

[**FltRetainSwappedBufferMdlAddress**](https://msdn.microsoft.com/library/windows/hardware/ff544352)

 

 




