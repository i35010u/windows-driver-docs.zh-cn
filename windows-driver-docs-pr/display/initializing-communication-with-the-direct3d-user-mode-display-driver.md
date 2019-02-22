---
title: 初始化 D3D 用户模式显示驱动程序通信
description: 初始化与 Direct3D 用户模式显示驱动程序的通信
ms.assetid: 96e85df4-e340-4017-b348-7c24349ffe69
keywords:
- 用户模式显示驱动程序 WDK Windows Vista 中，初始化
- Direct3D WDK 显示
- 用户模式显示驱动程序 WDK Windows Vista，Direct3D
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 0165c251a2c888339a7d3238d185c54a8ba2e542
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541898"
---
# <a name="initializing-communication-with-the-direct3d-user-mode-display-driver"></a>初始化与 Direct3D 用户模式显示驱动程序的通信

初始化与 Microsoft Direct3D 用户模式显示驱动程序，这是一个动态链接库 (DLL)，通信 Direct3D 运行时首次加载该 DLL。 Direct3D 运行时接下来将调用用户模式显示驱动程序[ **OpenAdapter** ](https://msdn.microsoft.com/library/windows/hardware/ff568601)函数通过 DLL 的导出表以打开图形适配器的实例。 *OpenAdapter*函数仅用于 DLL 的导出函数。

对驱动程序的调用中*OpenAdapter*函数，运行时会提供[ **pfnQueryAdapterInfoCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568920)适配器中的回调函数**pAdapterCallbacks**的成员[ **D3DDDIARG\_OPENADAPTER** ](https://msdn.microsoft.com/library/windows/hardware/ff543226)结构。 运行时还提供在其版本号**接口**并**版本**D3DDDIARG 成员\_OPENADAPTER。 用户模式显示驱动程序必须验证，它可以使用此版本的运行时。 用户模式显示驱动程序将返回一个表中其特定于适配器的函数**pAdapterFuncs** D3DDDIARG 成员\_OPENADAPTER。

用户模式显示驱动程序应调用[ **pfnQueryAdapterInfoCb** ](https://msdn.microsoft.com/library/windows/hardware/ff568920)适配器回调函数来查询的图形硬件功能中的显示微型端口驱动程序。

运行时调用用户模式显示驱动程序[ **CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540634)函数 （驱动程序的特定于适配器的功能之一） 创建用于处理集合的呈现状态和显示设备完成初始化。 初始化完成后，可以调用 Direct3D 运行时[显示驱动程序提供的函数](https://msdn.microsoft.com/library/windows/hardware/ff570118)，并且用户模式显示驱动程序可以调用[运行时提供的函数](https://msdn.microsoft.com/library/windows/hardware/ff552862)。

用户模式显示驱动程序*CreateDevice*使用调用函数[ **D3DDDIARG\_CREATEDEVICE** ](https://msdn.microsoft.com/library/windows/hardware/ff542931)中设置其成员的结构下面的方式来初始化用户模式显示驱动程序接口：

-   运行时设置**接口**到运行时需要从用户模式显示驱动程序接口的版本。

-   运行时设置**版本**驱动程序可用于标识时，运行时生成的数字。 例如，驱动程序可以使用的版本号随 Windows Vista 一起发布的运行时和后续的 service pack，其中可能包含驱动程序需要的修补程序发布的运行时之间进行区分。

-   运行时设置**hDevice**来指定当驱动程序回调到运行时，应使用该驱动程序的句柄。 该驱动程序生成唯一的句柄并将其传递到运行**hDevice**。 在运行时应使用返回**hDevice**处理后续的驱动程序调用。

-   运行时会提供在其设备特定的回调函数的表[ **D3DDDI\_DEVICECALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff544512)向其结构**pCallbacks**点。 用户模式显示驱动程序调用访问显示微型端口驱动程序中的内核模式服务的运行时提供的回调函数。

-   用户模式显示驱动程序将返回一个表中其特定于设备的函数[ **D3DDDI\_DEVICEFUNCS** ](https://msdn.microsoft.com/library/windows/hardware/ff544519)向其结构**pDeviceFuncs**点。

**请注意**  显示设备 （图形上下文中），可以同时存在数仅受可用系统内存。

 

 

 





