---
title: 识别适配器组和提供功能
description: 识别适配器组和提供功能
ms.assetid: 44a2ac71-8852-472f-82a2-7bd4d7dffa1a
keywords:
- 多头硬件 WDK DirectX 9.0，配置
- 多头硬件 WDK DirectX 9.0，适配器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 394bf0aebd46ed8dbc71cbec36ee80516b64d219
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839649"
---
# <a name="identifying-adapter-group-and-providing-capabilities"></a>识别适配器组和提供功能


## <span id="ddk_identifying_adapter_group_and_providing_capabilities_gg"></span><span id="DDK_IDENTIFYING_ADAPTER_GROUP_AND_PROVIDING_CAPABILITIES_GG"></span>


DirectX 9.0 运行时使用 D3DGDI2\_\_类型将**GetDriverInfo2**请求发送到 DirectX 9.0 版本驱动程序，以请求构成驱动程序的多头视频卡的适配器组的标识符. 驱动程序在[**DD\_GETADAPTERGROUPDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getadaptergroupdata)结构的**ulUniqueAdapterGroupId**成员中返回标识符。 驱动程序必须为组中的主适配器和所有从属适配器提供唯一标识符。 运行时在后续操作中使用此标识符来确定给定适配器是否是组的一部分。 此标识符必须在驱动程序（包括来自其他硬件供应商的驱动程序）中是唯一的。 因此，建议将此标识符报告为唯一的非零内核模式地址，此地址不能与其他多头视频卡相同。

DirectX 9.0 版本驱动程序通过设置 D3DCAPS9 结构的以下成员，指示其多头硬件的配置方式：

-   **NumberOfAdaptersInGroup**

    指定适配器组中的适配器数量（仅当 master）。 对于单层卡（传统适配器），这是1。 对于多头卡的主适配器，该值大于1。 对于多头卡的从属适配器，该值为0。 每张卡片最多只能有一个主节点，但可以有多个从属节点。

-   **MasterAdapterOrdinal**

    指定组中的主适配器的编号。 如果系统包含多个多个头卡，则此数字是相关的。 例如，如果系统包含一个卡、一个双头卡和一个三头卡，则系统会将 head 引用为：0（对于 double，为1和2），将3、4和5用于三级。 在这种情况下，主适配器为：0表示单个，1表示双精度，3表示三个。

-   **AdapterOrdinalInGroup**

    指定一个数字，该数字指示组中的头在由驱动程序引用的顺序。 对于主适配器，此值始终为0，对于每个从属适配器，此值为连续编号（即1、2等）。

驱动程序将返回 D3DCAPS9 结构，以响应**GetDriverInfo2**查询，如[报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持[GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

 

 





