---
title: 图像应用程序对话框扩展
description: 图像应用程序对话框扩展
ms.assetid: 4bb7d2f9-58c3-4cfa-aa6b-a4bd9335d2ac
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 343642d3ca7181c7cff77e042d3d7e3289015292
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193087"
---
# <a name="image-application-dialog-extensions"></a>图像应用程序对话框扩展





有三种机制可用于扩展 WIA 图像应用程序对话框。 这些方法包括：

-   在需要为设备显示图标的任何位置，提供一个用于替代系统提供的图标的设备图标。 为此，请实现 [**IWiaUIExtension：： GetDeviceIcon**](/previous-versions/windows/hardware/drivers/ff545075(v=vs.85)) 方法。

-   提供扩展系统提供的属性页的 [属性表扩展](property-sheet-extensions.md) ，当用户在公共 WIA 获取对话框或 Windows 资源管理器中查看设备的高级设置或属性时，将显示这些页。 为此，请实现 **IShellExtInit** 和 **IShellPropSheetExt** 接口 (参阅 Microsoft Windows SDK 文档) 。

-   为响应对 **IWiaItem：:D evicedlg** 的调用而显示的系统提供的对话框提供完全替换 (参见 Windows SDK 文档) 。 为此，请实现 [**IWiaUIExtension：:D evicedialog**](/previous-versions/windows/hardware/drivers/ff545069(v=vs.85)) 方法。

本部分的其余部分包含有关 [IWIAUIEXTENSION COM 接口](iwiauiextension-com-interface.md)的其他信息。

 

