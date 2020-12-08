---
title: 静态图像设备的属性表页面
description: 静态图像设备的属性表页面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3faa01c17ba0ec089b7448af27778d3322a20feb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829629"
---
# <a name="property-sheet-pages-for-still-image-devices"></a>静态图像设备的属性表页面





您可以提供一个 DLL 来创建特定于设备的属性页。 当用户尝试查看设备的属性表时，扫描仪和照相机控制面板会调用 DLL 的入口点。

若要使此 DLL 安装并使用，你必须在安装信息 (INF) 文件中包含一个 **PropertyPages** 条目。 此条目包含 DLL 的文件名和入口点名称。 有关详细信息，请参阅 [适用于静止图像设备的 INF 文件](inf-files-for-still-image-devices.md)。

 

 




