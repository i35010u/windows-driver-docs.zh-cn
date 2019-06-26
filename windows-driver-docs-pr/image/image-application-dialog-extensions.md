---
title: 图像应用程序对话框扩展
description: 图像应用程序对话框扩展
ms.assetid: 4bb7d2f9-58c3-4cfa-aa6b-a4bd9335d2ac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4acad15fb0dba025294369216ba9e40b55d5c95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363033"
---
# <a name="image-application-dialog-extensions"></a>图像应用程序对话框扩展





有三种机制来扩展 WIA 映像应用程序对话框。 这些问题包括：

-   提供设备图标，以代替中其中一个图标需要显示设备的任何位置的系统提供的图标。 若要执行此操作，实现[ **IWiaUIExtension::GetDeviceIcon** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545075(v=vs.85))方法。

-   提供[属性页扩展](property-sheet-extensions.md)扩展系统提供的属性页中，当用户查看高级的设置或设备的属性或 Windows 通用 WIA 获取对话框中显示资源管理器。 若要执行此操作，实现**IShellExtInit**并**IShellPropSheetExt**接口 （请参阅 Microsoft Windows SDK 文档）。

-   提供了完整的调用的响应中显示的系统提供的对话框**IWiaItem::DeviceDlg** （请参阅 Windows SDK 文档）。 若要执行此操作，实现[ **IWiaUIExtension::DeviceDialog** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545069(v=vs.85))方法。

本部分的其余部分包含有关其他信息[IWiaUIExtension COM 接口](iwiauiextension-com-interface.md)。

 

 




