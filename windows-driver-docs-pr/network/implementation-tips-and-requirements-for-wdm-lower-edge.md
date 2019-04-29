---
title: WDM 下边缘的实施提示和要求
description: WDM 下边缘的实施提示和要求
ms.assetid: 760c62ec-eeca-4b62-97ec-7cda5ee353a8
keywords:
- NDIS WDM 微型端口驱动程序 WDK 网络实现，以提示
- NDIS 微型端口驱动程序 WDK 网络驱动程序实现，以的下边缘
- WDM 低边缘 WDK 网络，驱动程序实现以
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ab16f15313e8369134d73c910ddb33a11daf261
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362563"
---
# <a name="implementation-tips-and-requirements-for-wdm-lower-edge"></a>WDM 下边缘的实施提示和要求





本主题介绍的提示和实现 NDIS WDM 微型端口驱动程序的要求。 NDIS WDM 微型端口驱动程序可以调用 NDIS 和非 NDIS 函数。 这些非 NDIS 函数包括，例如，WDM 内核模式支持例程和函数特定的总线驱动程序接口。

在实现 NDIS WDM 微型端口驱动程序时，请记住以下：

-   生成 NDIS WDM 微型端口驱动程序需要的 NDIS\_Ndis.h 标头文件是包含之前定义 WDM 标志。 定义 NDIS\_WDM 标志可确保 Ndis.h 会自动包括相应的 WDM 标头文件。 NDIS\_WDM 标志应是嵌入微型端口驱动程序的源代码的开头或微型端口驱动程序的源文件中设置。 NDIS WDM 微型端口驱动程序需要调用内核模式例程，例如 WDM 标头文件[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)并[ **IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257).

-   特定的总线驱动程序接口的函数调用需要针对该总线驱动程序的头文件。

-   不建议在同一源文件中包括 NDIS 和非 NDIS 标头，因为它们可能不兼容。 也就是说，调用 NDIS 函数的代码以及调用非 NDIS 函数的代码，则应创建单独的源代码文件。

-   NDIS WDM 微型端口驱动程序应调用适当的 NDIS 函数来分配和释放资源，除非 NDIS WDM 微型端口驱动程序分配和释放资源中的以下方案之一：

    -   资源，通常的内存资源分配的 NDIS WDM 微型端口驱动程序和更高版本的非 NDIS 实体的总线驱动程序接口，如通过发布
    -   非 NDIS 实体分配和更高版本发布的 NDIS WDM 微型端口驱动程序资源，通常的内存资源。

    对于上述方案，NDIS WDM 微型端口驱动程序应调用相应的 WDM 例程，以分配或释放非 NDIS 实体的资源。

 

 





