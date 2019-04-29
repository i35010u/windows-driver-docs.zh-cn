---
title: C28175
description: 警告的 C28175 结构的成员不应访问由驱动程序。
ms.assetid: 259a90d7-29ef-4a27-a921-8fff93b325bd
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28175
ms.openlocfilehash: bf336c3e89dd44cbaaf2a861650cc1007ca019fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361319"
---
# <a name="c28175"></a>C28175


警告 C28175:结构的成员不应访问由驱动程序

此警告指示驱动程序访问的驱动程序应永远不会访问的未记录的结构成员。

驱动程序应永远不会访问指定未记录的结构成员。 对于最未记录的不透明或半透明结构的成员，此禁止是绝对路径。 但是，驱动程序可能会访问从特定的例程中某些未记录的结构成员。 例如，驱动程序可以访问的未记录的成员的部分不透明[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)只在一个驱动程序中的结构\_INITIALIZE 或驱动程序\_卸载例程。

有时此规则适用于特定成员的原因并不明显。 例如，出现这种情况的一个实例是使用**NextDevice**的成员**\_设备\_对象**。 在本例中，锁应可以安全地访问此链接的列表，但该锁不是可用于驱动程序。 在这种情况下，违反此规则会导致很少，但硬诊断失败。 若要访问的相关的设备的正确方法是使用[ **IoEnumerateDeviceObjectList** ](https://msdn.microsoft.com/library/windows/hardware/ff548342)函数。

 

 





