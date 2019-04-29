---
title: 对象句柄和事件顺序
description: 对象句柄和事件顺序
ms.assetid: 5abbcda2-66cc-4460-99b6-e7796e65af68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5ecfa4de9f6cdf0670d56d197662a0ab8a32497
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379657"
---
# <a name="object-handle-and-event-order"></a>对象句柄和事件顺序





当 Microsoft PTP WIA 微型驱动程序发出**GetObjectHandles**命令 （请参阅 PIMA 15740 标准），照相机必须 WIA 微型驱动程序才能正确生成 WIA 项树以特定顺序返回对象句柄。

-   具有子对象的对象必须出现在前面及其子级的列表。

    句柄的数字顺序不重要。 例如，如果对象 5 有 4、 6 和 7 中，子对象列表应订购 5、 4、 6、 7。 排序 4、 5、 6、 7 不起作用。

-   对于辅助关联图像对象必须位于领先于其他对象的关联中的对象句柄列表。

-   ObjectRemoved 事件 （请参阅 PIMA 15740 标准） 必须按下向上的顺序出现。

    换而言之，直到由于 ObjectRemoved 事件已删除的所有子级，不应发生 ObjectRemoved 事件的对象。 如果内的辅助关联的图像将被删除，必须以响应 ObjectRemoved 事件中移除图像本身之前删除关联中的其他对象。

 

 




