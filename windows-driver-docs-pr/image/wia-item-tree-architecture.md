---
title: WIA 项树体系结构
description: WIA 项树体系结构
ms.assetid: 7e0f2b65-7150-4f8a-9780-abdaf93e44d6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39688f4367bf7c60f8b55d98ffe0a12dabf81fa5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555479"
---
# <a name="wia-item-tree-architecture"></a>WIA 项树体系结构





应用程序能够看到 WIA 项树是分开的树的创建和维护由 WIA 微型驱动程序。 当微型驱动程序创建的项的树时，WIA 服务使用此 WIA 项树作为指南来创建图像处理应用程序可以查看的相同副本。 复制树中的项目称为应用程序项目。 在树中创建的微型驱动程序的项目称为驱动程序项。

以下各节中提供了详细信息：

[应用程序项目和驱动程序项](application-items-and-driver-items.md)

[描述使用 WIA 项 WIA 设备](describing-a-wia-device-using-wia-items.md)

[更改 WIA 项树状结构](changing-the-wia-item-tree-structure.md)

 

 




