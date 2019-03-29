---
title: 上下文菜单扩展
description: 上下文菜单扩展
ms.assetid: 6c52dd43-7f47-476e-acbc-15269d23ea71
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8c3ed0b12339a922e786dbfa30f15e66d5281d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565398"
---
# <a name="context-menu-extensions"></a>上下文菜单扩展





扫描仪和照相机控件面板中的设备 （根项），并在我的电脑文件夹中的文件夹，用户可以选择要对选定的项目，根据其上下文菜单上公开的操作执行的各种操作。 若要查找这些操作，在用户右键单击缩略图或给定图像的图标。

将添加到上下文菜单上的操作的方法是实现**IContextMenu**接口 （请参阅 Microsoft Windows SDK 文档）。 供应商可以提供实现的进程内服务器**IContextMenu**接口**IWiaItem**设备提供的 （请参阅 Windows SDK 文档） 项。 每当 WIA 的图像的上下文菜单的查询，又调用供应商提供 UI 扩展插件**IContextMenu::QueryContextMenu**从为给定的图像处理设备注册的处理程序。 调用**IContextMenu::InvokeCommand**为项 UI 传递在默认情况下不处理打开到相应的供应商提供的扩展插件。

 

 




