---
title: 分段的筛选器简介
description: 分段的筛选器简介
ms.assetid: 3f73aa08-c3ef-4e97-9e3e-a1f0325cd599
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec74a5e0932326c049c8735c343cdb5b1239050f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523807"
---
# <a name="introduction-to-segmentation-filters"></a>分段的筛选器简介





分段筛选器是应用程序可用于分隔各个图片上的布局平板扫描仪，因此每个这些图片可以获取到单个映像的 WIA 扩展。 分段的筛选器是在应用程序的进程中运行的进程内 COM 组件。

分段筛选器是依赖于它所扩展的驱动程序。 驱动程序开发人员可以选择编写自己的分段筛选器或使用分段的筛选器，Microsoft 提供了与 Windows Vista 的开头。

支持的应用程序可以仅使用分段的筛选器[IStream 基于 WIA 传输模型](wia-transfer-architecture.md)。

下图显示了在应用程序的进程中运行的分段筛选器组件。

![说明在应用程序的进程中运行的分段筛选器组件的关系图](images/wia-components-app-process.png)

 

 




