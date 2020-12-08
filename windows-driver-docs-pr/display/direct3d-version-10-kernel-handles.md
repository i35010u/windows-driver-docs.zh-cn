---
title: Direct3D 版本 10 内核句柄
description: Direct3D 版本 10 内核句柄
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc1349afdc253888d3c30aee1fbe61b7891f62db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809429"
---
# <a name="direct3d-version-10-kernel-handles"></a>Direct3D 版本 10 内核句柄


Direct3D 版本10内核句柄生命周期通常由用户模式显示驱动程序显式控制。 此类句柄允许用户模式显示驱动程序操作分配。 此类控点还可以允许用户模式显示驱动程序与内核执行其他交互 (包括与显示微型端口驱动程序) 的交互。

下面显示了资源的内核句柄示例：

```cpp
// Strongly typed handle to identify a resource object to the driver: 
typedef struct D3D10DDI_HKMRESOURCE
{
    D3DKMT_HANDLE handle;
} D3D10DDI_HKMRESOURCE;
```

 

 





