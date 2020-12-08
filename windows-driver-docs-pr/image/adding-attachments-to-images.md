---
title: 将附件添加到图像
description: 将附件添加到图像
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c16b9ff596c08d8f8cb7a11990a11a803c1a672
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808293"
---
# <a name="adding-attachments-to-images"></a>将附件添加到图像





当项用 **WiaItemTypeHasAttachments** 标记时，这意味着该项具有关联的附件，它们存储为子项。 这不同于 **WiaItemTypeFolder** 类型的项。 它们的主要区别包括：

-   类型为 **WiaItemTypeHasAttachments** 的项只有一级子级。 **WiaItemTypeFolder** 类型的项可以有任意数量的子级。

-   类型为 **WiaItemTypeHasAttachments** 的项的所有子级都与该项相关。 例如，如果图像项具有关联的音频数据，则音频数据将存储为图像项的子元素，并且图像项将标记为 **WiaItemTypeHasAttachments**。

项不能同时为类型 **WiaItemTypeHasAttachments** 和类型 **WiaItemTypeFolder**。 但是，项可以是类型 **WiaItemTypeHasAttachments** ，类型 **WiaItemTypeFile**。 这是因为类型为 **WiaItemTypeHasAttachments** 的项在概念上被视为单个实体。 下图说明了包含附件的 WIA 相机项树。

![阐释带有附件的 wia 相机项树的关系图](images/camera-tree-attachments.png)

 

 




