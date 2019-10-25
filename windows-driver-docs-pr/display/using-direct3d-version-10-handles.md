---
title: 使用 Direct3D 版本 10 句柄
description: 使用 Direct3D 版本 10 句柄
ms.assetid: 98cde374-0267-44bc-b285-acf4a6d17ff4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0a82524cbe227250ae80a363153a9099c2781c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829261"
---
# <a name="using-direct3d-version-10-handles"></a>使用 Direct3D 版本 10 句柄


Direct3D 版本10句柄是强类型的，以防止 misusage 并使编译器检测到不匹配的句柄类型。 Direct3D 版本10句柄的生命周期从对 create type 函数（例如[**CreateGeometryShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_creategeometryshader)）的调用开始，并通过调用销毁类型函数（例如， [**DestroyShader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyshader)）结束。 Direct3D 版本10存在三种类型的句柄。 前两种类型的句柄是驱动程序句柄，Direct3D 运行时使用该句柄与驱动程序通信，并使用运行时句柄来与运行时进行通信。 图柄的第三个类别是内核句柄。 以下部分介绍了 Direct3D 版本10的句柄：

[Direct3D 版本10运行时和驱动程序句柄](direct3d-version-10-runtime-and-driver-handles.md)

[Direct3D 版本10内核句柄](direct3d-version-10-kernel-handles.md)

 

 





