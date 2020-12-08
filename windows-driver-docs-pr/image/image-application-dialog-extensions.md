---
title: 图像应用程序对话框扩展
description: 图像应用程序对话框扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cbba2f933d20eb8f3a4ca2a253819d0e1c89a4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793721"
---
# <a name="image-application-dialog-extensions"></a>图像应用程序对话框扩展





有三种机制可用于扩展 WIA 图像应用程序对话框。 其中包括：

-   在需要为设备显示图标的任何位置，提供一个用于替代系统提供的图标的设备图标。 为此，请实现 [**IWiaUIExtension：： GetDeviceIcon**](/previous-versions/windows/hardware/drivers/ff545075(v=vs.85)) 方法。

-   提供扩展系统提供的属性页的 [属性表扩展](property-sheet-extensions.md) ，当用户在公共 WIA 获取对话框或 Windows 资源管理器中查看设备的高级设置或属性时，将显示这些页。 为此，请实现 **IShellExtInit** 和 **IShellPropSheetExt** 接口 (参阅 Microsoft Windows SDK 文档) 。

-   为响应对 **IWiaItem：:D evicedlg** 的调用而显示的系统提供的对话框提供完全替换 (参见 Windows SDK 文档) 。 为此，请实现 [**IWiaUIExtension：:D evicedialog**](/previous-versions/windows/hardware/drivers/ff545069(v=vs.85)) 方法。

本部分的其余部分包含有关 [IWIAUIEXTENSION COM 接口](iwiauiextension-com-interface.md)的其他信息。

 

