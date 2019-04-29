---
title: 识别适配器组和提供功能
description: 识别适配器组和提供功能
ms.assetid: 44a2ac71-8852-472f-82a2-7bd4d7dffa1a
keywords:
- 多个头硬件 WDK DirectX 9.0 中，配置
- 多个头硬件 WDK DirectX 9.0 中，适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc59cc603954c3542e0f6baf27e4b0f1de48324e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384556"
---
# <a name="identifying-adapter-group-and-providing-capabilities"></a>识别适配器组和提供功能


## <span id="ddk_identifying_adapter_group_and_providing_capabilities_gg"></span><span id="DDK_IDENTIFYING_ADAPTER_GROUP_AND_PROVIDING_CAPABILITIES_GG"></span>


DirectX 9.0 运行时发送**GetDriverInfo2**请求使用 D3DGDI2\_类型\_GETADAPTERGROUP 值到 DirectX 9.0 版本驱动程序请求的标识符组成的适配器的组驱动程序的多个头视频卡。 驱动程序将返回中的标识符**ulUniqueAdapterGroupId**的成员[ **DD\_GETADAPTERGROUPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551529)结构。 该驱动程序必须为 master 和组中的所有从属适配器提供的唯一标识符。 运行时在后续操作中使用此标识符，以确定给定的适配器是否为组的一部分。 此标识符必须是唯一的驱动程序，包括其他硬件供应商提供的驱动程序。 因此，建议以不能为常见的其他多个头视频卡的唯一的非零内核模式地址的形式报告此标识符。

DirectX 9.0 版本驱动程序指示其多个头硬件通过设置以下 D3DCAPS9 结构的成员的配置方式：

-   **NumberOfAdaptersInGroup**

    （仅当 master) 适配器组中指定适配器的数。 这是 1 的单个头卡 （常规适配器）。 值为大于 1 的多个头卡的主适配器。 值为 0 的从属适配器的多个头卡。 每个卡可以具有最多一个主机，但可以有多个从属项。

-   **MasterAdapterOrdinal**

    指定组中主适配器的数量。 此数字是适用于系统包含多个多头卡。 例如，如果系统中包含单个头卡、 双头卡和 triple 头卡，系统将引用作为头：单个为 0、 1 和为双精度型、 2 和 3、 4 和 5 三重。 在这种情况下，主适配器是：单个为 0、 1 表示双精度型和三重为 3。

-   **AdapterOrdinalInGroup**

    指定一个数字，指示该驱动程序引用组中的头的顺序。 此值始终是主适配器为 0，为每个从属适配器连续编号 （即，1，2，依此类推）。

该驱动程序在响应中返回 D3DCAPS9 结构**GetDriverInfo2**查询类似于如何返回 D3DCAPS8 结构，如中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

 

 





