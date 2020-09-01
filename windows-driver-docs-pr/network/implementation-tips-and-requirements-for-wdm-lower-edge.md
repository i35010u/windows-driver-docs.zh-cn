---
title: WDM 下边缘的实施提示和要求
description: WDM 下边缘的实施提示和要求
ms.assetid: 760c62ec-eeca-4b62-97ec-7cda5ee353a8
keywords:
- NDIS-WDM 微型端口驱动程序 WDK 网络，实现提示
- NDIS 微型端口驱动程序的下边缘 WDK 网络，驱动程序实现
- WDM 低边缘 WDK 网络，驱动程序实现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f7a108401aac5181dd129d370c6738a4de3a49
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210739"
---
# <a name="implementation-tips-and-requirements-for-wdm-lower-edge"></a>WDM 下边缘的实施提示和要求





本主题介绍了实现 NDIS-WDM 微型端口驱动程序的提示和要求。 NDIS-WDM 微型端口驱动程序可以调用 NDIS 和非 NDIS 函数。 例如，对于特定的总线驱动程序接口，这些非 NDIS 函数包括 WDM 内核模式支持例程和函数。

实现 NDIS-WDM 微型端口驱动程序时，请记住以下事项：

-   生成 NDIS-WDM 微型端口驱动程序要求在 \_ 包含 ndis wdm 标志之前定义 ndis WDM 标志。 定义 NDIS \_ WDM 标志可确保 ndis 自动包含相应的 WDM 标头文件。 NDIS \_ WDM 标志应嵌入到微型端口驱动程序源代码的开头，或在微型端口驱动程序的源文件中设置。 NDIS-WDM 微型端口驱动程序需要 WDM 标头文件来调用内核模式例程，如 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 和 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)。

-   特定总线驱动程序接口的函数调用需要该总线驱动程序的标头文件。

-   不建议将 NDIS 和非 NDIS 标头包含在同一源文件中，因为它们可能不兼容。 也就是说，对于调用 NDIS 函数的代码和调用非 NDIS 函数的代码，应创建单独的源文件。

-   NDIS-WDM 微型端口驱动程序应调用适当的 NDIS 函数来分配和释放资源，除非 NDIS-WDM 微型端口驱动程序在以下其中一种情况下分配并释放资源：

    -   资源通常是内存资源，由 NDIS-WDM 微型端口驱动程序分配，稍后由非 NDIS 实体（如总线驱动程序接口）发布。
    -   资源通常是内存资源，由非 NDIS 实体分配，并稍后由 NDIS-WDM 微型端口驱动程序发布。

    对于上述方案，NDIS-WDM 微型端口驱动程序应调用相应的 WDM 例程，为非 NDIS 实体分配或释放资源。

 

