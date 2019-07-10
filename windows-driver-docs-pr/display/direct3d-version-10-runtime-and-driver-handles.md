---
title: Direct3D 版本 10 运行时和驱动程序句柄
description: Direct3D 版本 10 运行时和驱动程序句柄
ms.assetid: 1e50afe1-7103-45c4-8f58-a08d51423b22
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a3a1ebcc751ba8eb64412f5ba89564e192bab2e
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716870"
---
# <a name="direct3d-version-10-runtime-and-driver-handles"></a>Direct3D 版本 10 运行时和驱动程序句柄


Direct3D 10 版本运行时和驱动程序句柄共享相同的寿命范围。 Direct3D 运行时指定的创建类型函数的调用之间的对象的生存期 (例如， [ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)) 和对销毁类型函数的调用 (例如， [ **DestroyResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyresource))。 在运行时提供了驱动程序句柄值，以及运行时句柄值。 这些句柄是实质上是使用以确定于正在操作的对象的强类型包装的指针。 资源的运行时和驱动程序的句柄的示例如下：

```cpp
// Strongly typed handle to identify a resource object to the driver: 
typedef struct D3D10DDI_HRESOURCE
{
    void* pDrvPrivate; // Pointer to memory location as large as the driver requested.
} D3D10DDI_HRESOURCE;

// Strongly typed handle to identify a resource object to the runtime:
typedef struct D3D10DDI_HRTRESOURCE
{
    void* handle;
} D3D10DDI_HRTRESOURCE;
```

为呈现设备对象及其子对象的所有驱动程序句柄进行以下两个阶段创建机制：

1.  若要确定驱动程序句柄指针的值，则运行时首先调用_CalcPrivate_**ObjType**_大小_函数 (例如， [ **CalcPrivateResourceSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivateresourcesize)函数)。 在此调用中，运行时将创建参数中传递 (例如，指针[ **D3D10DDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createresource)结构)。 运行时还将在调用中的创建参数中传递_创建_**ObjType**函数。

    用户模式显示驱动程序通常不需要任何内容分配到的调用期间_CalcPrivate_**ObjType**_大小_。 但是，如果该驱动程序不和失败或者必须指示任何其他类型的失败条件，则驱动程序可以返回大小\_T (-1) 若要防止创建句柄。 然后，运行时会返回一个 E\_OUTOFMEMORY 错误条件调用应用程序。

    最小日志，则驱动程序应返回**sizeof (** void\* **)** 调用_CalcPrivate_**ObjType** _大小_。

2.  如果在运行时可以分配足够的空间来满足用户模式显示驱动程序，然后调用运行时，将需要的大小_创建_**ObjType**函数 (例如， [ **CreateResource(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createresource)) 使用相同的创建参数，以及驱动程序句柄的新唯一值。 驱动程序句柄的指针值将是唯一和常量的使用寿命的句柄，因为它指向的内存区域的大小已返回的_CalcPrivate_**ObjType** _大小_。 用户模式显示驱动程序可以根据需要使用此区域的内存。 驱动程序应通过增加获取的效率，通过定位到的运行时提供的内存区域经常访问的任何数据。

 

 





