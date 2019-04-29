---
title: WIA 相机树
description: WIA 相机树
ms.assetid: 8c932c91-b389-4b4c-b686-75ca6bf3de6a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec47b389a734dae8cccd9f2d0ac8e371b46e58af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390793"
---
# <a name="wia-camera-tree"></a>WIA 相机树





下图显示了包含多个映像，其中两个是相同的目录中的照相机。

![说明 camera 替换多个映像，其中两个是相同的目录中的关系图](images/art-camera.png)

在下图中，WIA 表示照相机照相机项的树形照相机，和任何文件夹拍摄的图片上图中所示。

![说明如何 wia 表示照相机照相机项的树形照相机，和任何文件夹拍摄的图片上图中所示的关系图](images/art-3.png)

根项，它是相机本身，包括通用设备属性 （照相机和扫描仪共有的属性） 和特定于照相机的设备属性。 同样，每个子项包括照相机和扫描仪项通用的属性，以及特定于照相机项的属性。

通过 WIA 的服务，应用程序可以从照相机项请求以下：

-   查询照相机功能。

-   设置相机的设备属性。

-   请求数据传输。

在上图中，相机根项具有三个子项： 两个图片和一个文件夹。 文件夹中有两个是这两个图片的子项目。 良好的数据或在照像机上的设备提供给应用程序的任何其他数据，还可以表示照相机的项。

 

 




