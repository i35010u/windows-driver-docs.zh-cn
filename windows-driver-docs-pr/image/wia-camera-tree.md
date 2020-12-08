---
title: WIA 相机树
description: WIA 相机树
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbc9346659d472587670a10ffc140ddf492f767b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831809"
---
# <a name="wia-camera-tree"></a>WIA 相机树





下图显示了包含多个图像的照相机，其中两个图像位于同一个目录中。

![说明具有多个图像的照相机的关系图，其中两个图像在同一目录中](images/art-camera.png)

在下图中，WIA 表示上图中显示的相机、使用照相机拍摄的图片以及将任何文件夹作为照相机项目的树。

![说明 wia 如何表示上图中显示的相机的关系图、使用照相机拍摄的图片以及作为照相机项树的任何文件夹](images/art-3.png)

根项是照相机本身，它包含 (照相机和扫描仪) 的通用设备属性以及相机特定设备属性。 同样，每个子项都包含照相机和扫描仪项共有的属性，以及特定于照相机项的属性。

通过 WIA 服务，应用程序可以从照相机项目请求以下内容：

-   查询相机功能。

-   设置照相机设备属性。

-   请求数据传输。

在上图中，照相机根项包含三个子项：两个图片和一个文件夹。 文件夹包含两个子项，它们都是图片。 相机项还可以表示设备在应用程序中提供的声音数据或相机上的任何其他数据。

 

 




