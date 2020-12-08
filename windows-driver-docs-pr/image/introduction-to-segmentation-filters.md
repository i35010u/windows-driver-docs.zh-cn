---
title: 分段筛选器简介
description: 分段筛选器简介
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ddf69914741b8e15ae9f550a4834c8c9ec74bdd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828691"
---
# <a name="introduction-to-segmentation-filters"></a>分段筛选器简介





分段筛选器是一个 WIA 扩展，应用程序可以使用它来分离平板扫描仪上布局的各个图片，以便可以将这些图片中的每个图片都采集到各个图像中。 分段筛选器是在应用程序的进程中运行的进程内 COM 组件。

分段筛选器取决于它所扩展的驱动程序。 驱动程序开发人员可以选择编写自己的分段筛选器，也可以使用 Microsoft 从 Windows Vista 开始提供的分段筛选器。

仅支持 [基于 IStream 的 WIA 传输模型](wia-transfer-architecture.md)的应用程序可以使用分段筛选器。

下图显示了在应用程序的进程中运行的分段筛选器组件。

![说明在应用程序进程中运行的分段筛选器组件的关系图](images/wia-components-app-process.png)

 

 




