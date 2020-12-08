---
title: C28176
description: 警告 C28176 结构成员不应由驱动程序修改。
keywords:
- 列出用于驱动程序的 WDK PREfast 的警告
- 为驱动程序列出的 WDK PREfast 的错误
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28176
ms.openlocfilehash: 67754ef9c5fc03b3274b29059a1f1c9bc7ea43cd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808497"
---
# <a name="c28176"></a>C28176


警告 C28176：结构的成员不应由驱动程序修改

此警告表明驱动程序更改了驱动程序不应更改的未记录的结构成员。

驱动程序不应写入指定的未记录的结构成员。 对于不透明或部分不透明结构的大多数未记录的成员，此禁止是绝对的。 但是，驱动程序可能会在特定例程内编写某些未记录的结构成员。 例如， [**设备 \_ 对象。**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object) 只能在驱动程序 \_ 初始化或驱动程序卸载例程内编写 NextDevice 成员 \_ 。

 

