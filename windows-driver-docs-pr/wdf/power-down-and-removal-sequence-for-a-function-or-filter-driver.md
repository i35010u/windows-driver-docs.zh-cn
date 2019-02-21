---
title: 电源关闭和删除序列的函数或筛选器驱动程序
description: 电源关闭和删除序列的函数或筛选器驱动程序
ms.assetid: E5A22C91-5967-42D6-A991-42B46C72ED82
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b5a0af13f2c8bfdd379ebbcfa0a6aafe0abbbe9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554518"
---
# <a name="power-down-and-removal-sequence-for-a-function-or-filter-driver"></a>电源关闭和删除序列的函数或筛选器驱动程序


下图显示了在其中框架将调用 KMDF 函数或筛选器驱动程序的事件回调函数时关闭和删除设备的顺序。 在序列图顶部开头操作设备处于工作电源状态 (D0):

![函数或筛选器驱动程序的电源关闭和删除序列](images/fdo-fido-powerdown3.png)

如图所示，KMDF 电源关闭和删除序列涉及调用在导致设备操作，包括在其中框架调用的函数的相反顺序对应"撤消"回调。 框架中删除的设备对象后删除设备对象上下文区域。

 

 





