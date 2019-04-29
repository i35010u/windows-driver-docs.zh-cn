---
title: Direct3D 版本 10 内核句柄
description: Direct3D 版本 10 内核句柄
ms.assetid: 48378f27-4c08-4931-9592-878a1a2b2556
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a791f97207085246cbc82549022fbb20f4b4b10f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357969"
---
# <a name="direct3d-version-10-kernel-handles"></a>Direct3D 版本 10 内核句柄


Direct3D 版本 10 内核句柄生命范围通常由控制用户模式显示驱动程序显式。 此类的句柄允许用户模式显示驱动程序来操作分配。 此类的句柄也可以允许用户模式显示驱动程序执行内核 （包括与显示微型端口驱动程序的交互） 与其他交互。

下面显示了资源的内核句柄的示例：

```cpp
// Strongly typed handle to identify a resource object to the driver: 
typedef struct D3D10DDI_HKMRESOURCE
{
    D3DKMT_HANDLE handle;
} D3D10DDI_HKMRESOURCE;
```

 

 





