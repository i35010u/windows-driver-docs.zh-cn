---
title: Direct3D 版本 10.1 的版本号
description: Direct3D 版本 10.1 的版本号
ms.assetid: a121900a-49e9-40f6-a3a6-d391e3bf1e37
keywords:
- Direct3D 版本 10.1 WDK 显示版本号
- 版本号 WDK 显示
- 版本号 WDK 显示，Direct3D 版本 10.1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f36e35a3c5a1dba214c9106f245403647ad43f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374337"
---
# <a name="version-numbers-for-direct3d-version-101"></a>Direct3D 版本 10.1 的版本号


Direct3D 版本 10.0 和 10.1 供应\#定义用户模式显示驱动程序使用的版本控制功能。 用户模式显示驱动程序必须检查**接口**的成员[ **D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)， [ **D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)，和[ **D3D10DDIARG\_CALCPRIVATEDEVICESIZE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_calcprivatedevicesize)结构的驱动程序在调用接收[ **OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)， [ **CreateDevice(D3D10)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)，和[ **CalcPrivateDeviceSize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)函数来确定的 Direct3D 运行时支持 Direct3D DDI 的版本。 最重要的 16 位**接口**成员是 Direct3D DDI 主要版本的版本号。 有关 Direct3D 版本 10.0 和 10.1，此数字是 10。 最重要的 16 位**接口**成员是 Direct3D DDI 次要版本。 每次引入的重大更改 Direct3D DDI 是已升级此次要版本值。 此次要版本值可以也会解除了一个人为地以表示更强大的版本更改。 以下\#发行的版号定义关联的 Direct3D DDI 次要版本 (即，D3D10\_0 = = x，D3D10\_1 = = y，其中 y &gt; x)。

用户模式显示驱动程序应仅检查最重要的 16 位**版本**的成员[ **D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)， [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)，并[ **D3D10DDIARG\_CALCPRIVATEDEVICESIZE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_calcprivatedevicesize)到结构确定构建 Direct3D 运行时。 每次发生了非换行 Direct3D DDI 变化时，此值是手动增长。 该驱动程序可能来自要取决于每个非换行 DDI 随时间发生。 因此，应确保该驱动程序传入 DDI 的生成版本是大于或等于\*\_生成\_版本当前驱动程序和是否故障的驱动程序不兼容 (也许是同时还提供注册表的解决方法）。 最重要的 16 位**版本**成员是 DDI 修订版本。 最重要的 16 位**版本**常用于将驱动程序基于 Direct3D API 中存在的 bug 的特殊情况。 该驱动程序必须成功创建的所有值。 但是，该驱动程序可以更改取决于特定值的行为。 应使用这些值与比较&gt;=，因为这些数字可能由于运行时修补程序任意上升。 此外，不应使用"&gt; （以前中断的版本）"(而非"&gt;= 工作版本") 因为新修订可能会出现已知的两个数字之间的版本号并不包含所需的修复。 以下\#定义适用于 Direct3D DDI 版本控制：

```cpp
#define D3D10_DDI_MAJOR_VERSION 10
#define D3D10_0_DDI_MINOR_VERSION 1
#define D3D10_0_DDI_INTERFACE_VERSION ((D3D10_DDI_MAJOR_VERSION << 16) | D3D10_0_DDI_MINOR_VERSION)
#define D3D10_0_DDI_BUILD_VERSION 4
#define D3D10_0_DDI_VERSION_VISTA_GOLD                          ( ( 4 << 16 ) | 6000 )
#define D3D10_0_DDI_VERSION_VISTA_GOLD_WITH_LINKED_ADAPTER_QFE  ( ( 4 << 16 ) | 6008 )
#define D3D10_0_DDI_IS_LINKED_ADAPTER_QFE_PRESENT(Version)  (Version >= D3D10_0_DDI_VERSION_VISTA_GOLD_WITH_LINKED_ADAPTER_QFE)

#if D3D10DDI_MINOR_HEADER_VERSION >= 1
#define D3D10_1_DDI_MINOR_VERSION 2
#define D3D10_1_DDI_INTERFACE_VERSION ((D3D10_DDI_MAJOR_VERSION << 16) | D3D10_1_DDI_MINOR_VERSION)
#define D3D10_1_DDI_BUILD_VERSION 1
// Note: d3d10_1 doesn't currently ship on vista gold. // This definition is included for completeness in the 
// event that it does at some point in the future:
#define D3D10_1_DDI_VERSION_VISTA_GOLD                          ( ( 1 << 16 ) | 6000 )
#define D3D10_1_DDI_VERSION_VISTA_SP1                           ( ( 1 << 16 ) | 6008 )
#define D3D10_1_DDI_IS_LINKED_ADAPTER_QFE_PRESENT(Version)  (Version >= D3D10_1_DDI_VERSION_VISTA_SP1)

#define D3D10on9_DDI_MINOR_VERSION 0
#define D3D10on9_DDI_INTERFACE_VERSION ((D3D10_DDI_MAJOR_VERSION << 16) | D3D10on9_DDI_MINOR_VERSION)
#define D3D10on9_DDI_BUILD_VERSION 0
```

 

 





