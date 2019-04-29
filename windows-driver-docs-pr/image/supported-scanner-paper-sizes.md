---
title: 支持的扫描仪纸张大小
description: 支持的扫描仪纸张大小
ms.assetid: c4437c38-b43a-433c-913a-d3de9bf74284
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 026bd09af83f5f147128dd7e68cce0def86571c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322277"
---
# <a name="supported-scanner-paper-sizes"></a>支持的扫描仪纸张大小





尽管两个 WIA 用户界面组件能够向用户显示页面大小的列表，但没有 WIA 驱动程序以了解扫描仪支持的页大小的简单的方法。

### <a name="page-size-in-wia-applications"></a>WIA 应用程序中的页面大小

允许为支持报表页大小的 WIA 驱动程序没有 WIA 属性或允许直接指定页大小的应用程序。 若要进行通信到驱动程序的页面大小设置，应用程序必须计算所需的大小，以每英寸点数 (dpi) 并调整扫描以符合设备的注册要求的来源。

### <a href="" id="page-size-in-the-common-scanner-dialog-and-in-the-scanner-and-camera-w"></a>页面大小和扫描仪和照相机向导中常见的扫描程序对话框

常见的扫描程序对话框和扫描仪和照相机向导具有一个静态表中的每个页大小所述按水平宽度和垂直高度，增量为 0.001 英寸都受支持的页大小。 仅当扫描程序是在文档送纸器模式下时，当前会显示这些页大小。

由平台最大大小，最大页大小 （按区域） 驱动程序支持在页面源模式下，被视为默认页面大小。 不适合在送纸器或设备的平台上的纸张大小不会提供给用户。

 

 




