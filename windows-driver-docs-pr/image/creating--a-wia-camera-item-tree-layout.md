---
title: 创建 WIA 相机项树布局
description: 创建 WIA 相机项树布局
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: e40ca670c9b06aad013ffa5c71e583d637205524
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839263"
---
# <a name="creating-a-wia-camera-item-tree-layout"></a>创建 WIA 相机项树布局

适用于 Microsoft Windows Me 和 Windows XP 的 WIA 摄像机项树包含一个根项以及表示照相机设备上存储的图像和文件夹的子项。 有关如何创建项树的示例，请参阅 [初始化 WIA 微型驱动程序](initializing-the-wia-minidriver.md) 。 下图显示了 Windows Me 和 Windows XP 的项树。

![说明用于 windows me 和 windows xp 的 wia 相机项树的关系图](images/camera-tree.png)

有关 Windows Vista 和更高版本操作系统中的相机树的图示，请参阅 [WIA 项标志和类别的示例用法](example-usage-of-wia-item-flags-and-categories.md)。

相机项树的根项包含所有标准 WIA 微型驱动程序信息和相机特定属性。 相机特定属性包括拍摄的图片数和其他相机控件属性。

相机项树的子项表示设备上存储的图像或文件夹。 建议微型驱动程序删除任何不必要的文件夹级别，以便更轻松地访问可转让的项目。 这使得应用程序能够更轻松地访问 WIA 项，并防止用户在文件夹结构中导航到实际图像。

微型驱动程序开发人员可以为文件和文件夹项指定所需的任何名称。 但是，WIA 项树中的每一项都表示相机上的物理数据项，应为其指定一个建议照相机中实际数据项的名称。

当在照相机中添加或删除数据项时，WIA 微型驱动程序负责将其 WIA 项树与照相机内容同步。 有关如何执行此操作的示例，请参阅 [更改 WIA 项树结构](changing-the-wia-item-tree-structure.md)。

通过 WIA 服务，应用程序可以执行以下操作：

- 查询照相机功能

- 设置照相机设备属性

- 请求数据传输
