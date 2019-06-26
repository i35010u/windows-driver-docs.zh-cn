---
title: C28176
description: 警告的 C28176 结构的成员不应修改由驱动程序。
ms.assetid: 837b2dcd-0682-460f-a3ae-ebd82bcc451b
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28176
ms.openlocfilehash: bbf48ababf2ce0be16ea35978aa91b76de5dc1d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371477"
---
# <a name="c28176"></a>C28176


警告 C28176:结构的成员不应修改由驱动程序

此警告指示驱动程序更改驱动程序应永远不会更改的未记录的结构成员。

驱动程序不应写入指定的未记录的结构成员。 对于最未记录的不透明或半透明结构的成员，此禁止是绝对路径。 但是，驱动程序可以编写从特定的例程中某些未记录的结构成员。 例如， [**设备\_对象。NextDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)可以仅在一个驱动程序中编写成员\_INITIALIZE 或驱动程序\_卸载例程。

 

 





