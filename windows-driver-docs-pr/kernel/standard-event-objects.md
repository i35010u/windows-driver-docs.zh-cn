---
title: 标准事件对象
description: 标准事件对象
ms.assetid: 3c34c485-28b1-45d5-9e79-05dd2b26015e
keywords:
- 事件对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9cc0dcdc85fa64da826fc4ffefc936ed1be310d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569495"
---
# <a name="standard-event-objects"></a>标准事件对象





系统提供了几个标准事件对象。 驱动程序可以使用这些事件对象时出现某些特定情况由系统得到通知。 以下列表包含的标准事件对象：

<a href="" id="-kernelobjects-highmemorycondition"></a>**\\KernelObjects\\HighMemoryCondition**  
可用物理内存量超过系统定义的量时，将设置此事件。 驱动程序可以等待要设置作为主动的方式分配内存的信号发出此事件。

<a href="" id="-kernelobjects-lowmemorycondition"></a>**\\KernelObjects\\LowMemoryCondition**  
可用物理内存量低于系统定义的量时，将设置此事件。 已分配的内存量大的驱动程序可以等待该事件作为信号来释放未使用的内存设置。

有关 Microsoft Windows Server 2003 和更高版本的 Windows，驱动程序还可以使用以下其他标准事件对象：

<a href="" id="-kernelobjects-highpagedpoolcondition"></a>**\\KernelObjects\\HighPagedPoolCondition**  
免费页面缓冲池的数量超过系统定义的量时，将设置此事件。 驱动程序可以等待要设置作为主动的方式从页面缓冲池分配内存的信号发出此事件。

<a href="" id="-kernelobjects-lowpagedpoolcondition"></a>**\\KernelObjects\\LowPagedPoolCondition**  
每当免费页面缓冲池的量低于系统定义的量时，将设置此事件。 已分配的内存量大的驱动程序可以等待该事件作为信号来释放未使用的内存中分页池设置。

<a href="" id="-kernelobjects-highnonpagedpoolcondition"></a>**\\KernelObjects\\HighNonPagedPoolCondition**  
可用的非分页池量超过系统定义的量时，将设置此事件。 驱动程序可以等待要设置作为主动的方式从非分页缓冲池分配内存的信号发出此事件。

<a href="" id="-kernelobjects-lownonpagedpoolcondition"></a>**\\KernelObjects\\LowNonPagedPoolCondition**  
可用的非分页池的量低于系统定义的量时，将设置此事件。 已分配的内存量大的驱动程序可以等待该事件作为信号来释放未使用的内存从非分页缓冲池设置。

对于 Windows Vista 和更高版本的 Windows，驱动程序还可以使用以下其他标准事件对象：

<a href="" id="-kernelobjects-lowcommitcondition"></a>**\\KernelObjects\\LowCommitCondition**  
将设置此事件 operating system*提交费用*较低，相对于*当前提交限制*。 换而言之，内存使用率较低，大量的空间可在物理内存或分页文件中。

<a href="" id="-kernelobjects-highcommitcondition"></a>**\\KernelObjects\\HighCommitCondition**  
操作系统的提交费用较高，相对于当前的提交限制时，将设置此事件。 换而言之，内存使用率较高和极少的空间可在物理内存或分页文件中，但操作系统可能能够增加其分页文件的大小。

<a href="" id="-kernelobjects-maximumcommitcondition"></a>**\\KernelObjects\\MaximumCommitCondition**  
如果操作系统的内存附近，则设置此事件*最大提交限制*。 换而言之，内存使用率较高非常小的空间可用物理内存或分页文件中，是操作系统不能增加其分页文件的大小。 （系统管理员可以始终会增加的大小或数量的分页文件，无需重新启动计算机，如果存在足够的存储资源）。

每个事件是通知事件。 只要触发条件保持为 true，则它们保持设置。

若要打开的句柄任一这些事件，请使用[ **IoCreateNotificationEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff549039)例程。 等待任何这些事件的驱动程序应创建专用的线程执行等待。 线程可以等待一个或多个这些事件通过调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)或[ **KeWaitForMultipleObjects**](https://msdn.microsoft.com/library/windows/hardware/ff553324)。

 

 




