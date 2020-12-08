---
title: 使用标准漫射光的环境贴图
description: 使用标准漫射光的环境贴图
keywords:
- 映射多维数据集环境
- 环境映射 WDK Direct3D
- 多维数据集环境映射 WDK Direct3D
- 照明 WDK Direct3D
- 漫射照明 WDK Direct3D
- 标准漫射照明 WDK Direct3D
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: c3b8d8621363adebf285a006fd110e2ec7d616aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792327"
---
# <a name="environment-mapping-with-standard-diffuse-lighting"></a>使用标准漫射光的环境贴图

可在几何管道中执行漫射组件 Gouraud 底纹的标准漫射照明计算。 但是，为了获得最佳的真实性，反射组件可通过多维数据集环境映射来生成。 当两者都处于操作中时，应用程序指定的 [FVF](fvf--flexible-vertex-format-.md) 应在照明计算位置中包含一个向量，并将单独的3d 纹理坐标集用作多维数据集映射中的矢量。

 

 





