---
title: Bug 检查 0x4D NO_PAGES_AVAILABLE
description: NO_PAGES_AVAILABLE bug 检查的值为0x0000004D。 这表示无可用页面可用于继续操作。
keywords:
- Bug 检查 0x4D NO_PAGES_AVAILABLE
- NO_PAGES_AVAILABLE
ms.date: 12/27/2018
topic_type:
- apiref
api_name:
- NO_PAGES_AVAILABLE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b2ec618b2c34cbe1264d847c6cd4e14fad0356a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831643"
---
# <a name="bug-check-0x4d-no_pages_available"></a>Bug 检查0x4D：无 \_ \_ 可用页


"无 \_ 可用页" \_ bug 检查的值为0x0000004D。 这表示无可用页面可用于继续操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="no_pages_available-parameters"></a>无 \_ \_ 可用页参数

|参数|描述|
|--- |--- |
|1|脏页总数|
|2|发往页面文件的脏页数|
|3|发生 bug 检查时可用的非分页池的大小|
|4|最近修改的写入错误状态。|


<a name="cause"></a>原因
-----

若要查看一般内存统计信息，请使用 [**！ vm 3**](-vm.md) 扩展。

由于以下任一原因，可能会发生此错误检查：

-   驱动程序已阻止，死锁已修改或映射的页编写器。 这种情况的示例包括互斥锁或对文件系统驱动程序或筛选器驱动程序中的内存分页的访问。 这表明驱动程序 bug。

    如果参数1或参数2很大，则可能会出现这种情况。 使用 [**！ vm 3**](-vm.md)。

-   存储驱动程序未处理请求。 这种情况的示例包括：闲置队列和无响应驱动器。 这表明驱动程序 bug。

    如果参数1或参数2很大，则可能会出现这种情况。 使用 [**！ vm 8**](-vm.md)，后跟 [**！ process 0 7**](-process.md)。

-   高优先级实时线程会耗尽了平衡集管理器从工作集中修整页面，或会耗尽修改后的页面写入器将其写入。这表示创建此线程的组件中的 bug。

    这种情况很难进行分析。 尝试使用 [**！ ready**](-ready.md)。 请尝试 [**操作！处理 0 7**](-process.md) 以列出所有线程，并查看是否有累积过多的内核时间以及其当前优先级。 此类进程可能已阻止内存管理线程使页面可用。

-  没有足够的池可用于存储堆栈，无法写出已修改的页面。 这表明驱动程序 bug。

    如果参数3较小，则可能是这样。 使用 [**！ vm**](-vm.md) 和 [**！ poolused 2**](-poolused.md)。

如果找不到该问题，请尝试使用从开始处连接的内核调试器启动，并监视这种情况。

 

 




