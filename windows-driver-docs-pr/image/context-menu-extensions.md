---
title: 上下文菜单扩展
description: 上下文菜单扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6689d604f641d902332076e4a7a0b5e96c6f62bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831817"
---
# <a name="context-menu-extensions"></a>上下文菜单扩展





在设备的 "扫描仪和照相机" 控制面板文件夹中 (根项) ，而在我的电脑文件夹中，用户可以根据其上下文菜单上公开的操作选择要对选定项执行的各种操作。 若要查找这些操作，用户可以右键单击给定图像的缩略图或图标。

向上下文菜单中的操作添加的方法是实现 **IContextMenu** 接口 (参阅 Microsoft Windows SDK 文档) 。 供应商可以提供实现 **IWiaItem** 的 **IContextMenu** 接口的进程内服务器 (参阅该设备提供) 项的 Windows SDK 文档。 只要 WIA 查询图像的上下文菜单，供应商提供的 UI 扩展就会从为给定的图像处理设备注册的处理程序中调用 **IContextMenu：： QueryContextMenu** 。 对于不由默认 UI 处理的项，对 **IContextMenu：： invokecommand 启动** 的调用将被传递给相应的供应商提供的扩展。

 

 




