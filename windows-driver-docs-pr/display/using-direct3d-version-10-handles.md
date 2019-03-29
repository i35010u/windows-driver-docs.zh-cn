---
title: 使用 Direct3D 版本 10 句柄
description: 使用 Direct3D 版本 10 句柄
ms.assetid: 98cde374-0267-44bc-b285-acf4a6d17ff4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04f98cb90cacd05c75dc14c0043a08da16dc9f62
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575586"
---
# <a name="using-direct3d-version-10-handles"></a>使用 Direct3D 版本 10 句柄


Direct3D 版本 10 句柄是强类型，以防止 misusage 并启用编译器以检测不匹配的句柄类型。 10 个句柄已开始对创建类型函数的调用的有效期的 Direct3D 版本 (例如， [ **CreateGeometryShader**](https://msdn.microsoft.com/library/windows/hardware/ff540648))，结尾对破坏类型函数的调用 (例如， [ **DestroyShader**](https://msdn.microsoft.com/library/windows/hardware/ff552805))。 Direct3D 版本 10 存在三种类别的句柄。 句柄的前两个类别是 Direct3D 运行时使用与该驱动程序进行通信，驱动程序句柄和运行时句柄，该驱动程序使用与运行时进行通信。 句柄的第三个类别是内核句柄。 以下部分介绍的 Direct3D 版本 10 句柄：

[Direct3D 版本 10 运行时和驱动程序句柄](direct3d-version-10-runtime-and-driver-handles.md)

[Direct3D 版本 10 内核句柄](direct3d-version-10-kernel-handles.md)

 

 





