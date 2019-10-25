---
title: NDIS 6.60 简介
description: 本部分介绍了 NDIS 6.60，并介绍了 NDIS 6.50 中的更改。 NDIS 6.60 包含在 Windows 10、版本1607和 Windows Server 2016 及更高版本中。
ms.assetid: AFDFD1CD-2E07-4A4F-82E2-5E6C5AABD5A3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae9374d3aacd415bc282d2496525d96859cdb325
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844168"
---
# <a name="introduction-to-ndis-660"></a>NDIS 6.60 简介

本主题介绍网络驱动程序接口规范（NDIS）6.60，并介绍其主要的设计添加内容。 NDIS 6.60 包含在 Windows 10、版本1607和 Windows Server 2016 及更高版本中。

NDIS 6.60 是 NDIS 6.50 的次要版本更新。 有关将 NDIS 1.x 驱动程序移植到 NDIS 6.60 的详细信息，请参阅[将 ndis 1.x 驱动程序移植到 ndis 6.60](porting-ndis-6-x-drivers-to-ndis-6-60.md)。

## <a name="feature-updates"></a>功能更新

NDIS 6.60 是 NDIS 6.50 的增量更新，不包含任何主要的新功能。

## <a name="implementing-an-ndis-660-driver"></a>实现 NDIS 6.60 驱动程序

NDIS 6.60 驱动程序必须遵循在[实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中定义的要求。

此外，NDIS 6.60 驱动程序必须符合以下要求：

- 当 ndis 6.60 驱动程序使用 NDIS 注册时，它必须报告正确的 NDIS 版本。
   
   必须更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 结构中的主要和次要 NDIS 版本号，才能支持 NDIS 6.60。 MajorNdisVersion 成员必须包含6个，并且 MinorNdisVersion 成员必须包含60。 此要求适用于微型端口、协议和筛选器驱动程序。 还必须更新编译器的版本信息（请参阅[编译 NDIS 6.60 驱动程序](#compiling-an-ndis-660-driver)）。

- 适用于 Windows 10、版本1607和 Windows Server 2016 及更高版本的 NDIS 6.60 微型端口驱动程序必须使用 NDIS 6.60 版本的数据结构。 有关详细信息，请参阅[使用 NDIS 6.60 数据结构](#using-ndis-660-data-structures)。

## <a name="compiling-an-ndis-660-driver"></a>编译 NDIS 6.60 驱动程序

适用于 Windows 10 版本1607的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.60 驱动程序在编译时使用合适的 NDIS 6.60 数据结构。

将以下编译器设置添加到你的驱动程序的 Visual Studio 项目中：

- 对于微型端口驱动程序，请添加 ```NDIS660_MINIPORT=1```。
- 对于筛选器或协议驱动程序，请添加 ```NDIS660=1```。

有关使用 Windows 10 1607 版的 WDK 构建驱动程序的信息，请参阅[构建驱动程序](../develop/building-a-driver.md)。

## <a name="using-ndis-660-data-structures"></a>使用 NDIS 6.60 数据结构

### <a name="updated-data-structures"></a>更新的数据结构

以下数据结构已在 NDIS 6.60 中更新。

- [NDIS_NIC_SWITCH_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)
- [NDIS_RECEIVE_SCALE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)
- [NDIS_RECEIVE_SCALE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)

