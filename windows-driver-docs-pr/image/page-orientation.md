---
title: 页面方向
description: 页面方向
ms.assetid: fb28863a-920a-4b26-a652-fb255622824f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18814746f04783600801f5f2e60b19fc26f77867
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327869"
---
# <a name="page-orientation"></a>页面方向


WIA 微型驱动程序必须确保 WIA\_IP\_ORIENTATION 属性同意与当前所选内容区域。 如果应用程序更改的值 WIA\_IP\_方向设为一个无效的当前所选的页面大小，微型驱动程序应更改 WIA 的值\_IP\_页\_到页面大小新的方向值支持的大小。

请注意，如果[ **WIA\_IPS\_方向**](https://msdn.microsoft.com/library/windows/hardware/ff552625)设置 LANSCAPE，将"翻转。"的范围设置为 例如，如果应用程序设置 WIA\_IPS\_页面\_WIA 的大小\_页\_A4，微型驱动程序应设置[ **WIA\_IP\_页\_宽度**](https://msdn.microsoft.com/library/windows/hardware/ff552636)到 11692 和[ **WIA\_IP\_页\_高度**](https://msdn.microsoft.com/library/windows/hardware/ff552632) 8267 到。 (微型驱动程序还应设置[ **WIA\_IPS\_大 XEXTENT** ](https://msdn.microsoft.com/library/windows/hardware/ff552661)并[ **WIA\_IP\_YEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552669)相应。)请注意，如果 WIA\_IPS\_页面\_大小设置为 WIA\_页\_自定义，方向设置不用于确定要扫描的页的区域维度。

 

 




