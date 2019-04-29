---
title: 页面大小和方向
description: 页面大小和方向
ms.assetid: f744a00c-8614-4488-9a29-d193a0c4268f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb14620afd918ce89f50fc0c9843f8fa92fe2d08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392621"
---
# <a name="page-size-and-orientation"></a>页面大小和方向


扫描程序设置页大小和方向是相互关联。 同时确定将扫描的页的大小。

例如，页大小和扩展盘区使用的值 WIA\_PROP\_列表取决于有效的设置的 WIA\_IP\_ORIENTATION 属性。 因此，如果设备无法扫描具有 WIA 横向的文档\_页上\_A4 设置，WIA\_页面\_A4 不应出现在列表中的有效值为 WIA\_IP\_页\_大小属性时 WIA\_IP\_方向将设置为 LANSCAPE。

值[ **WIA\_IPS\_方向**](https://msdn.microsoft.com/library/windows/hardware/ff552625)属性确定当前所选页面的方向。 [ **WIA\_IPS\_页\_高度**](https://msdn.microsoft.com/library/windows/hardware/ff552632)并[ **WIA\_IP\_页\_宽度**](https://msdn.microsoft.com/library/windows/hardware/ff552636)属性报告页面的尺寸，以英寸为单位的千分之几秒 (。 001)。 这些 height 和 width 属性必须包含等效于中的值的值[ **WIA\_IPS\_大 XEXTENT** ](https://msdn.microsoft.com/library/windows/hardware/ff552661)并[ **WIA\_IPS\_YEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552669)，它提供的信息以像素为单位的页面的尺寸。

有关使用页大小和方向的详细信息，请参阅以下主题：

[受支持的扫描程序纸张大小](supported-scanner-paper-sizes.md)

[自定义和自动页面大小](custom-and-auto-page-sizes.md)

[页面方向](page-orientation.md)

[扫描程序的页大小和方向的代码示例](page-size-and-orientation-code-examples.md)

 

 




