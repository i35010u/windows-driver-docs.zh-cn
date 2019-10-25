---
title: Direct3D 版本 10.1 的版本号
description: Direct3D 版本 10.1 的版本号
ms.assetid: a121900a-49e9-40f6-a3a6-d391e3bf1e37
keywords:
- Direct3D 版本 10.1 WDK 显示，版本号
- WDK 显示的版本号
- 版本编号 WDK 显示，Direct3D 版本10。1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a56ddd184d08d7046fef04d4403df799516bfe6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829214"
---
# <a name="version-numbers-for-direct3d-version-101"></a>Direct3D 版本 10.1 的版本号


Direct3D 版本10.0 和10.1 供应 \#定义用户模式显示驱动程序用于版本控制。 用户模式显示驱动程序必须检查[**D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)， [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)和 D3D10DDIARG 的**Interface**成员， [ **\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_calcprivatedevicesize)驱动程序接收到[**OpenAdapter10**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)、 [**CreateDevice （D3D10）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)和[**CalcPrivateDeviceSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)函数的调用，以确定 DIRECT3D 运行时支持的 direct3d DDI 版本。 **接口**成员最有效的16位是 Direct3D DDI 主版本的数目。 对于 Direct3D 版本10.0 和10.1，此数为10。 **接口**成员的最小有效16位是 Direct3D DDI 次要版本。 此次要版本值在引入 Direct3D DDI 重大更改时已升级。 此次要版本值还可以已升级人为表示更强的版本更改。 以下 \#定义与已发布版本号（即，D3D10\_0 = = x，D3D10\_1 = = y，其中 y &gt; x）关联的 Direct3D DDI 次版本。

用户模式显示驱动程序只应检查[**D3D10DDIARG\_OPENADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)、 [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)和 D3D10DDIARG 的**版本**成员的最重要16位[ **\_CALCPRIVATEDEVICESIZE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_calcprivatedevicesize)结构来确定 Direct3D 运行时的生成时间。 此值将在每次发生非中断的 Direct3D DDI 更改时手动已升级。 驱动程序可能取决于每次不间断的 DDI 更改。 因此，驱动程序应确保传入的 DDI 生成版本大于或等于 \*\_生成当前驱动程序的\_版本，并在驱动程序不兼容的情况下（可能同时提供注册表解决方法时）进行故障排除。 **版本**成员的16位最低有效版本为 DDI 版本。 最小有效的16位**版本**通常用于基于 Direct3D API 中存在的 bug 的特殊情况。 对于所有值，驱动程序必须成功创建。 但是，驱动程序可能会根据特定值更改行为。 应使用 &gt;= 来比较这些值，因为这些数字可能会因为运行时修复而任意增加。 此外，不应使用 "&gt; （以前的损坏版本）" （而不是 "&gt;= 工作版本"），因为新版本可能会显示在两个已知数字之间有版本号，并且不包含所需的修补程序。 以下 \#用于 Direct3D DDI 版本控制：

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

 

 





