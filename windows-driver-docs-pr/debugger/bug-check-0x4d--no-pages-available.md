---
title: Bug 检查就将 0x4D NO_PAGES_AVAILABLE
description: NO_PAGES_AVAILABLE bug 检查具有 0x0000004D 值。 这表明没有可用的空闲页是可用于继续操作。
ms.assetid: c1f8fb33-a01c-4455-87a7-59aa6ba7cb37
keywords:
- Bug 检查就将 0x4D NO_PAGES_AVAILABLE
- NO_PAGES_AVAILABLE
ms.date: 12/27/2018
topic_type:
- apiref
api_name:
- NO_PAGES_AVAILABLE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 062a3525bce8a9a3de5ccbb385760a2b9fc0ccf8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363469"
---
# <a name="bug-check-0x4d-nopagesavailable"></a>Bug 检查 0x4D：否\_页面\_可用


否\_页面\_可用 bug 检查的值为 0x0000004D。 这表明没有可用的空闲页是可用于继续操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="nopagesavailable-parameters"></a>否\_页面\_可用参数

|参数|描述|
|--- |--- |
|1|脏页的总数|
|2|为页面文件发送到的损坏页的数量|
|3|检查错误发生的时可用的非分页池的大小|
|4|最新修改写入错误状态。|


<a name="cause"></a>原因
-----

若要查看常规内存统计信息，请使用[ **！ vm 3** ](-vm.md)扩展。

此 bug 检查可能发生以下情况之一：

-   已阻止驱动程序，死锁已修改或映射页编写器。 此示例包括互斥锁死锁或访问文件系统驱动程序或筛选器驱动程序中的内存分页。 这指示驱动程序 bug。

    如果参数 1 或参数 2 很大，这是可能。 使用[ **！ vm 3**](-vm.md)。

-   存储驱动程序不处理请求。 此示例是孤立的队列和非响应驱动器。 这指示驱动程序 bug。

    如果参数 1 或参数 2 很大，这是可能。 使用[ **！ vm 8**](-vm.md)后, 跟[ **！ 处理 0 7**](-process.md)。

-   高优先级实时线程会耗尽出工作集修整页中的均衡集管理器或会耗尽从写出的已修改的页编写器。这表示创建此线程的组件中存在 bug。

    这种情况下很难分析。 请尝试使用[ **！ 准备**](-ready.md)。 此外可以尝试[ **！ 处理 0 7** ](-process.md)列出所有线程，并请参阅是否但任何累积了过多的内核时间以及其当前的优先级是什么。 此类进程可能已阻止出提供页面的内存管理线程。

-  没有足够的池是可用于存储堆栈，写出已修改页。 这指示驱动程序 bug。

    如果参数 3 很小，这是可能。 使用[ **！ vm** ](-vm.md)并[ **！ poolused 2**](-poolused.md)。

如果找不到问题，然后尝试通过内核调试程序附加从一开始，启动和监视这种情况。

 

 




