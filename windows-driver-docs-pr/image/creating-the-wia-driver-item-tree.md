---
title: 创建 WIA 驱动程序项树
description: 创建 WIA 驱动程序项树
ms.assetid: 3ae489b9-175e-4b1e-a6c8-a72a3a3c212a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0be7c0f885bc398e3b552b4e80c5d1634c890b2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191714"
---
# <a name="creating-the-wia-driver-item-tree"></a>创建 WIA 驱动程序项树





初始化微型驱动程序后，必须通过以下方式在 [**IWiaMiniDrv：:D rvinitializewia**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia) 方法中创建驱动程序项树：

1.  如果驱动程序项树尚不存在，则创建它。 微型驱动程序设置根项标志，并通过调用驱动程序服务库函数 [**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)创建根项。 微型驱动程序将返回的指针存储到私有成员变量中的根项。

2.  使用 [**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem) 函数为设备上的每个项创建子项目。 此函数创建设备特定的上下文，微型驱动程序可以在此上下文中存储有关项的信息。

3.  对每个子项调用 [**IWiaDrvItem：： AddItemToFolder**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiadrvitem-additemtofolder) 方法，将该项添加到驱动程序项树中。

 

