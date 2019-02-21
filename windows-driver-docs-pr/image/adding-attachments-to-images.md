---
title: 将附件添加到映像
description: 将附件添加到映像
ms.assetid: 704f541b-b98c-44a8-bb19-5d5d0d1eab78
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8946c0775106ea6b0436b767a4cdcc0acf629b31
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524407"
---
# <a name="adding-attachments-to-images"></a>将附件添加到映像





当某项将标有**WiaItemTypeHasAttachments**，这意味着在于项具有关联的附件，它们将存储为子项目。 这不是相同类型的项**WiaItemTypeFolder**。 主要差异有：

-   类型的项**WiaItemTypeHasAttachments**具有只有一个级别的子级。 类型的项**WiaItemTypeFolder**可以有任意数量的级别的子级。

-   类型的项的所有子级**WiaItemTypeHasAttachments**与该项相关。 例如，如果某一图像项具有关联的音频数据，将作为图像项的子存储音频数据和图像项会标记有**WiaItemTypeHasAttachments**。

项不能为这两个类型**WiaItemTypeHasAttachments**并键入**WiaItemTypeFolder**。 但是，项可以为类型**WiaItemTypeHasAttachments**并键入**WiaItemTypeFile**。 这是因为类型的项**WiaItemTypeHasAttachments**从概念上讲视为单个实体。 下图演示了带有附件的 WIA 照相机项树。

![说明带有附件的 wia 照相机项树的关系图](images/camera-tree-attachments.png)

 

 




