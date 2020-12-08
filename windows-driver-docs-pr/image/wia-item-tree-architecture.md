---
title: WIA 项树体系结构
description: WIA 项树体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: debed1389f31065f428515b221cfd043093e6ac2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826525"
---
# <a name="wia-item-tree-architecture"></a>WIA 项树体系结构





应用程序可以看到的 WIA 项树独立于由 WIA 微型驱动程序创建和维护的树。 当微型驱动程序创建项树时，WIA 服务使用此 WIA 项树作为创建可由图像应用程序查看的相同副本的指南。 复制树中的项称为应用程序项。 微型驱动程序创建的树中的项称为 "驱动程序项"。

有关详细信息，请访问以下部分：

[应用程序项和驱动程序项](application-items-and-driver-items.md)

[使用 WIA 项描述 WIA 设备](describing-a-wia-device-using-wia-items.md)

[更改 WIA 项树状结构](changing-the-wia-item-tree-structure.md)

 

 




