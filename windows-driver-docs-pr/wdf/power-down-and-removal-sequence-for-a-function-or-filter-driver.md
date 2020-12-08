---
title: 函数或筛选器驱动程序的电源关闭和删除顺序
description: 函数或筛选器驱动程序的电源关闭和删除顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdeefc95aca9f365544e905bc54c43f4dbab1e50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796381"
---
# <a name="power-down-and-removal-sequence-for-a-function-or-filter-driver"></a>函数或筛选器驱动程序的电源关闭和删除顺序


下图显示了在关闭和删除设备时，框架调用 KMDF 函数或筛选器驱动程序的事件回调函数的顺序。 序列从图形顶部开始，其操作设备处于工作电源状态 (D0) ：

![函数或筛选器驱动程序的关机和删除顺序](images/fdo-fido-powerdown3.png)

如图所示，KMDF 关闭和删除序列涉及到按与使设备正常运行所涉及的函数的相反顺序调用相应的 "撤消" 回调。 框架在删除设备对象上下文区域后删除设备对象。

 

 





