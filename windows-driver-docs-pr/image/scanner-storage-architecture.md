---
title: 扫描仪存储体系结构
description: 扫描仪存储体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d11bb427194c20fc5f0b8111165c2574bb4d984
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785193"
---
# <a name="scanner-storage-architecture"></a>扫描仪存储体系结构


配有一个或多个存储单元的扫描仪设备应该在其 WIA 项树中至少实现一个根存储文件夹扫描器项 (WIA \_ 类别 \_ 文件夹) ，以表示所有可用存储单元的一个单独的存储单元或逻辑根。 在存储根项下，可能有一些子文件夹项 (WIA \_ category \_ FOLDER) ，它代表单个存储单元 (如果所有存储单元均映射到存储单元上的该唯一存储根项) 或文件夹中的文件文件夹，而各个文件项 (WIA \_ 类别 \_ 完成 \_ 文件) 。

**注意**   根存储文件夹扫描程序项应直接位于 WIA 根项的位置。 根存储文件夹项可能包含其他文件夹项和文件，也可能为空。

 

仅配备空存储单元的扫描程序 (例如，不包含任何数据的内部硬盘驱动器) 应具有如下图所示的 WIA 项树。

![说明包含空存储单元的扫描仪的项目树的关系图](images/wia-storage-tree-simple.png)

上图是一个不包含扫描仪项目的简化图形。 扫描仪上至少有一个扫描仪项 (平板、进纸器或胶卷) ，任何类型的扫描仪都可能配有存储，如下图所示。

![说明包含存储的平板扫描仪的项目树的关系图](images/wia-storage-tree1.png)

上图显示了扫描仪的 WIA 项树，该树支持平板影印扫描以及包含一个子文件夹和两个文件的存储单元。

 

 




