---
title: 使用标准漫射光的环境贴图
description: 使用标准漫射光的环境贴图
ms.assetid: 7cdba0db-fdaf-46a4-a5f9-c5e930f68314
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
ms.openlocfilehash: 8f92b2945d89652fec2d35f323020a579cb6d998
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363104"
---
# <a name="environment-mapping-with-standard-diffuse-lighting"></a>使用标准漫射光的环境贴图

可以在几何管道中执行标准漫射照明计算高氏着色的漫射组件。 但是，对于最佳的真实性，可以通过多维数据集环境映射生成反射分量。 两者都是在操作中，当[FVF](fvf--flexible-vertex-format-.md)指定的应用程序应包含一个向量中的位置进行照明计算，并在多维数据集映射中用作向量将设置的单独三维纹理坐标。

 

 





