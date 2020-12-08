---
title: WIA 驱动程序项树
description: WIA 驱动程序项树
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc8b0b3946d7d98e8a2ab81eaf75a85750f1bd89
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822331"
---
# <a name="wia-driver-item-tree"></a>WIA 驱动程序项树





在 WIA 中，图像处理设备以逻辑方式表示为 WIA 项的层次结构树，如相机树的下图所示。

![阐释 wia 驱动程序项树的关系图](images/art-2.png)

根项表示实际设备，子项表示图像或文件夹。 文件夹可以包含图像或其他文件夹。 项具有微型驱动程序可以设置或查询的属性。

通过 WIA 服务，应用程序使用项来执行此类任务，如获取和设置设备信息、控制设备以及启动驱动程序项枚举。

应用程序可以调用 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 方法，通过从项请求数据传输来从项获取数据。

 

