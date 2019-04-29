---
title: WIA 驱动程序项树
description: WIA 驱动程序项树
ms.assetid: 67232179-4b9b-49a0-b8b0-5ed0914d4156
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 241e5b28472b23cddcfef2b1fe1669b4bb439d61
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366882"
---
# <a name="wia-driver-item-tree"></a>WIA 驱动程序项树





在 WIA，成像设备表示逻辑上作为 WIA 项的层次结构树照相机树的以下关系图中所示。

![说明 wia 驱动程序项树的关系图](images/art-2.png)

根项表示实际设备，并且子项目表示图像或文件夹。 文件夹可以包含图像或其他文件夹。 项具有微型驱动程序可以设置或查询的属性。

学习 WIA 服务，应用程序使用某项执行获取和设置设备信息、 控制该设备，并启动驱动程序项枚举等任务。

应用程序可以调用[ **IWiaMiniDrv::drvAcquireItemData** ](https://msdn.microsoft.com/library/windows/hardware/ff543956)方法来通过数据传输请求的项目中获取数据项的数据。

 

 




