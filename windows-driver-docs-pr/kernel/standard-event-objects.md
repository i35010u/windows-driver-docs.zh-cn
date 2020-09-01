---
title: 标准事件对象
description: 标准事件对象
ms.assetid: 3c34c485-28b1-45d5-9e79-05dd2b26015e
keywords:
- 事件对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ed60a3a9a22b28d92a1ed195db36be7b7d57193
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185789"
---
# <a name="standard-event-objects"></a>标准事件对象





系统提供若干标准事件对象。 当出现特定情况时，驱动程序可以使用这些事件对象来接收系统通知。 下面的列表包含标准事件对象：

<a href="" id="-kernelobjects-highmemorycondition"></a>**\\KernelObjects \\ HighMemoryCondition**  
只要可用物理内存量超过系统定义的数量，就会设置此事件。 驱动程序可以等待将此事件设置为主动分配内存的信号。

<a href="" id="-kernelobjects-lowmemorycondition"></a>**\\KernelObjects \\ LowMemoryCondition**  
只要可用物理内存量低于系统定义的数量，就会设置此事件。 分配了大量内存的驱动程序可以等待将此事件设置为可释放未使用内存的信号。

对于 Microsoft Windows Server 2003 和更高版本的 Windows，驱动程序还可以使用以下附加标准事件对象：

<a href="" id="-kernelobjects-highpagedpoolcondition"></a>**\\KernelObjects \\ HighPagedPoolCondition**  
只要可用分页池的数量超过系统定义的数量，就会设置此事件。 驱动程序可以等待将此事件设置为发出信号，以主动从页面池分配内存。

<a href="" id="-kernelobjects-lowpagedpoolcondition"></a>**\\KernelObjects \\ LowPagedPoolCondition**  
只要可用分页池的数量低于系统定义的数量，就会设置此事件。 分配了大量内存的驱动程序可以等待将此事件设置为从页面池中释放未使用的内存的信号。

<a href="" id="-kernelobjects-highnonpagedpoolcondition"></a>**\\KernelObjects \\ HighNonPagedPoolCondition**  
只要可用非分页池的数量超过系统定义的数量，就会设置此事件。 驱动程序可以等待将此事件设置为从非分页池主动分配内存的信号。

<a href="" id="-kernelobjects-lownonpagedpoolcondition"></a>**\\KernelObjects \\ LowNonPagedPoolCondition**  
只要可用非分页池的数量低于系统定义的数量，就会设置此事件。 分配了大量内存的驱动程序可以等待将此事件设置为从非分页池释放未使用的内存的信号。

对于 Windows Vista 和更高版本的 Windows，驱动程序还可以使用以下附加标准事件对象：

<a href="" id="-kernelobjects-lowcommitcondition"></a>**\\KernelObjects \\ LowCommitCondition**  
此事件在操作系统的 *提交费用* 低时设置，相对于 *当前的提交限制*。 换句话说，内存使用量较低，物理内存或页面文件中提供了大量空间。

<a href="" id="-kernelobjects-highcommitcondition"></a>**\\KernelObjects \\ HighCommitCondition**  
此事件在操作系统的提交费用较高时设置，相对于当前的提交限制。 换句话说，内存使用量很高，物理内存或页面文件中的可用空间非常小，但操作系统可能会增加页面文件的大小。

<a href="" id="-kernelobjects-maximumcommitcondition"></a>**\\KernelObjects \\ MaximumCommitCondition**  
当操作系统的提交费用接近 *最大 commit 限制*时，将设置此事件。 换句话说，内存使用量非常高，物理内存或页面文件中的可用空间非常小，操作系统无法增加其分页文件的大小。  (系统管理员始终可以增加页面文件的大小或数量，而无需重新启动计算机（如果存在足够的存储资源）。 ) 

其中每个事件都是通知事件。 只要触发条件保持为 true，它们就会保持设置。

若要打开任何这些事件的句柄，请使用 [**IoCreateNotificationEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatenotificationevent) 例程。 等待其中任何事件的驱动程序应创建一个专用线程来执行等待。 线程可以通过调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 或 [**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)等待一个或多个此类事件。

 

