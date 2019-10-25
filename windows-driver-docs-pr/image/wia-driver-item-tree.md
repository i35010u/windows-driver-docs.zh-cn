---
title: WIA 驱动程序项树
description: WIA 驱动程序项树
ms.assetid: 67232179-4b9b-49a0-b8b0-5ed0914d4156
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5d0438807f4f2a8fc7cbd5095fc89ce6edc95e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840707"
---
# <a name="wia-driver-item-tree"></a>WIA 驱动程序项树





在 WIA 中，图像处理设备以逻辑方式表示为 WIA 项的层次结构树，如相机树的下图所示。

![阐释 wia 驱动程序项树的关系图](images/art-2.png)

根项表示实际设备，子项表示图像或文件夹。 文件夹可以包含图像或其他文件夹。 项具有微型驱动程序可以设置或查询的属性。

通过 WIA 服务，应用程序使用项来执行此类任务，如获取和设置设备信息、控制设备以及启动驱动程序项枚举。

应用程序可以调用[**IWiaMiniDrv：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法，通过从项请求数据传输来从项获取数据。

 

 




