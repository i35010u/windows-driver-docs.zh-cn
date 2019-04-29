---
title: 静态图像设备的属性表页面
description: 静态图像设备的属性表页面
ms.assetid: ef77e57d-f791-4afa-8d51-67e78b60cf57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c459ae18b2b3ae6788c1e5462516d7eb6189e8e1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379641"
---
# <a name="property-sheet-pages-for-still-image-devices"></a>静态图像设备的属性表页面





您可以创建特定于设备的属性表页的 DLL。 扫描仪和照相机控件面板调用 DLL 的入口点，当用户尝试查看设备的属性表。

若要使此 DLL 才能安装和使用，必须包括**属性页**将安装程序信息 (INF) 文件中的条目。 此条目包含 DLL 的文件的名称和入口点名称。 有关详细信息，请参阅[静止图像设备 INF 文件](inf-files-for-still-image-devices.md)。

 

 




