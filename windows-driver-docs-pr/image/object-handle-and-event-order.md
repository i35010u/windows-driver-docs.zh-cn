---
title: 对象句柄和事件顺序
description: 对象句柄和事件顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74f94d139914e19fd9fc88ba949b71bfcd1bd19c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829635"
---
# <a name="object-handle-and-event-order"></a>对象句柄和事件顺序





当 Microsoft PTP WIA 微型驱动程序发出 **GetObjectHandles** 命令时 (参阅 pima indian diabetes 15740 标准) ，照相机必须按特定顺序返回对象句柄，以便 wia 微型驱动程序正确生成 wia 项树。

-   具有子对象的对象在其子级之前必须出现在列表中。

    句柄的数值顺序并不重要。 例如，如果 object 5 具有子对象4、6和7，则列表应按5、4、6、7进行排序。 顺序4、5、6、7将不起作用。

-   对于辅助关联，图像对象必须位于关联中其他对象之前的对象句柄列表中。

-   ObjectRemoved 事件 (参阅 PIMA INDIAN DIABETES 15740 standard) 必须按下向上的顺序出现。

    换句话说，对象的 ObjectRemoved 事件不会发生，除非 ObjectRemoved 事件已删除所有子级。 如果要删除辅助关联中的映像，则必须删除关联中的其他对象，以响应 ObjectRemoved 事件，然后再删除图像本身。

 

 




