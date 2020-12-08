---
title: Direct3D 版本 10.1 的版本号
description: Direct3D 版本 10.1 的版本号
keywords:
- Direct3D 版本 10.1 WDK 显示，版本号
- WDK 显示的版本号
- 版本编号 WDK 显示，Direct3D 版本10。1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd43988da4387452cbb0acac266ab99a1ba07063
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796219"
---
# <a name="version-numbers-for-direct3d-version-101"></a>Direct3D 版本 10.1 的版本号


Direct3D 版本10.0 和10.1 提供 \# 定义用户模式显示驱动程序用于版本控制。 用户模式显示驱动程序必须检查 [**D3D10DDIARG \_ OPENADAPTER**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)、 [**D3D10DDIARG \_ CREATEDEVICE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)和 [**D3D10DDIARG \_ CALCPRIVATEDEVICESIZE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_calcprivatedevicesize)结构的 **接口** 成员，驱动程序会在调用 [**OpenAdapter10**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_openadapter)、 [**CREATEDEVICE (D3D10)**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createdevice)和 [**CALCPRIVATEDEVICESIZE**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivatedevicesize)函数时接收该成员，以确定 direct3d 运行时支持的 direct3d DDI 版本。 **接口** 成员最有效的16位是 Direct3D DDI 主版本的数目。 对于 Direct3D 版本10.0 和10.1，此数为10。 **接口** 成员的最小有效16位是 Direct3D DDI 次要版本。 此次要版本值在引入 Direct3D DDI 重大更改时已升级。 此次要版本值还可以已升级人为表示更强的版本更改。 下面的 \# 定义将 DIRECT3D DDI 次要版本与已发布版本号 (即，D3D10 \_ 0 = = x，D3D10 \_ 1 = = y，其中，y &gt; x) 相关联。

用户模式显示驱动程序只应检查 [**D3D10DDIARG \_ OPENADAPTER**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_openadapter)、 [**D3D10DDIARG \_ CREATEDEVICE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)和 [**D3D10DDIARG \_ CALCPRIVATEDEVICESIZE**](/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_calcprivatedevicesize)结构的 **版本** 成员的最高有效16位，才能确定 Direct3D 运行时的生成时间。 此值将在每次发生非中断的 Direct3D DDI 更改时手动已升级。 驱动程序可能取决于每次不间断的 DDI 更改。 因此，当驱动程序不兼容时，驱动程序应确保传入的 DDI 生成版本大于或等于 \* \_ \_ 当前驱动程序的内部版本，如果驱动程序不兼容 (可能会失败，同时还提供注册表解决方法) 。 **版本** 成员的16位最低有效版本为 DDI 版本。 最小有效的16位 **版本** 通常用于基于 Direct3D API 中存在的 bug 的特殊情况。 对于所有值，驱动程序必须成功创建。 但是，驱动程序可能会根据特定值更改行为。 应使用 = 比较这些值， &gt; 因为这些数字可能会因为运行时修复而任意增加。 此外，不应使用 " &gt; (以前的损坏版本) " (而不是 " &gt; = 工作版本" ) ，因为新版本可能出现在两个已知数字之间且不包含所需的修补程序。 以下 \# 定义适用于 DIRECT3D DDI 版本管理：

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

 

