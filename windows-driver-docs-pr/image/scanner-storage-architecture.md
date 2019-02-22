---
title: 扫描程序存储体系结构
description: 扫描程序存储体系结构
ms.assetid: 90b2367f-c611-47c6-bd60-4125bd7ca709
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f439a6f9e6a52806c4581b636fcdf3ed6cb5fb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554863"
---
# <a name="scanner-storage-architecture"></a>扫描程序存储体系结构


配备了一个或多个存储单元的扫描程序设备应实现至少一个根存储文件夹扫描程序项目 (WIA\_类别\_文件夹) 中其 WIA 项树来表示一个单独的存储单元或逻辑所有可用的存储单元的根。 在存储根项，可能有子文件夹项 (WIA\_类别\_文件夹)，表示单个存储单元 （如果此唯一的存储根项下映射所有存储单元） 或文件的存储单元上的文件夹和各个文件项 (WIA\_类别\_已完成\_文件)。

**请注意**  根存储文件夹扫描程序项应位于直接来自 WIA 根项。 根存储文件夹项可能包含其他文件夹项和文件，也可能是空。

 

扫描程序配备有只是空的存储单元 （例如，内部硬盘驱动器，不包含任何数据） 应拥有类似于下图的 WIA 项树。

![说明与空存储单元的扫描仪的项树的关系图](images/wia-storage-tree-simple.png)

上图中是没有扫描程序项目的简化的图形。 扫描程序将具有至少一个扫描程序项 （平板、 送纸器或电影胶片） 和任何类型的扫描程序装配存储，如下图所示。

![说明使用存储平板扫描仪项树的关系图](images/wia-storage-tree1.png)

上图显示了支持平板辊扫描的扫描仪和包含一个子文件夹和两个文件的存储单元的 WIA 项树。

 

 




