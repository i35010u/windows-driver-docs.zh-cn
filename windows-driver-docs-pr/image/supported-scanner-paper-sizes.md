---
title: 支持的扫描仪纸张大小
description: 支持的扫描仪纸张大小
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2b52097018ebcf28f010433720b13c23121d3bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816185"
---
# <a name="supported-scanner-paper-sizes"></a>支持的扫描仪纸张大小





尽管两个 WIA 用户界面组件能够向用户显示一系列页面大小，但无法通过 WIA 驱动程序来了解扫描仪支持的页面大小。

### <a name="page-size-in-wia-applications"></a>WIA 应用程序中的页面大小

没有 WIA 属性允许 WIA 驱动程序报告受支持的页面大小或允许应用程序直接指定页面大小。 若要将页面大小设置传达给驱动程序，应用程序必须以每英寸点数 (dpi) 来计算所需大小，并调整扫描的源以符合设备的注册要求。

### <a name="page-size-in-the-common-scanner-dialog-and-in-the-scanner-and-camera-wizard"></a><a href="" id="page-size-in-the-common-scanner-dialog-and-in-the-scanner-and-camera-w"></a>常见扫描器对话框和扫描仪和照相机向导中的页面大小

常见的 "扫描仪" 对话框和 "扫描仪和照相机向导" 都有一个受支持页面大小的静态表，其中每个页面大小都按其水平宽度和垂直高度（以0.001 英寸为增量）进行描述。 仅当扫描程序处于文档送纸器模式时，才会显示这些页面大小。

按区域 (的最大页面大小) ，驱动程序在页面进纸模式下支持的页面大小（由最大床大小确定）被视为默认页面大小。 不适合进纸器或设备平台上的纸张大小不会提供给用户。

 

 




