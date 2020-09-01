---
title: WIA 驱动程序项树
description: WIA 驱动程序项树
ms.assetid: 67232179-4b9b-49a0-b8b0-5ed0914d4156
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f2de1679d9bdfc88e56ee26196ce1d8058362a5
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185019"
---
# <a name="wia-driver-item-tree"></a>WIA 驱动程序项树





在 WIA 中，图像处理设备以逻辑方式表示为 WIA 项的层次结构树，如相机树的下图所示。

![阐释 wia 驱动程序项树的关系图](images/art-2.png)

根项表示实际设备，子项表示图像或文件夹。 文件夹可以包含图像或其他文件夹。 项具有微型驱动程序可以设置或查询的属性。

通过 WIA 服务，应用程序使用项来执行此类任务，如获取和设置设备信息、控制设备以及启动驱动程序项枚举。

应用程序可以调用 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 方法，通过从项请求数据传输来从项获取数据。

 

