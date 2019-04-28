---
title: NDIS 6.70 简介
description: 本部分介绍 NDIS 6.70，并介绍了从 NDIS 6.60 的更改。 NDIS 6.70 包含在 Windows 10，版本 1703年。
ms.assetid: D846EE68-2C84-40E0-91DE-2034F75D576F
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91c955a03143d8f96d7c01dc4d47090ed41cb7ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349459"
---
# <a name="introduction-to-ndis-670"></a>NDIS 6.70 简介

本主题介绍网络驱动程序接口规范 (NDIS) 6.70 并描述其主要设计新增功能。 NDIS 6.70 包含在 Windows 10，版本 1703年。

NDIS 6.70 是次要版本更新到 NDIS 6.60 微型端口、 协议、 筛选器和中间驱动程序。 有关移植到 NDIS 6.70 NDIS 6.x 驱动程序的详细信息，请参阅[移植 NDIS 6.x 驱动程序到 NDIS 6.70](porting-ndis-6-x-drivers-to-ndis-6-70.md)。

## <a name="feature-updates"></a>功能更新

### <a name="netadaptercx"></a>NetAdapterCx

以及 NDIS 6.70，Windows 10 版本 1703年包括名为网络适配器 WDF 类扩展，也称为 NIC 驱动程序的重要新增功能 [NetAdapterCx](../netcx/index.md)。 NetAdapterCx 为预览版，仅在 Windows 10，版本 1703年中。 NetAdapterCx 模型使 NIC 驱动程序开发人员能够利用完整的功能和简化的驱动程序模型的 WDF，更轻松地编写含义 NIC 驱动程序。

### <a name="other-feature-updates"></a>其他功能更新

NDIS 窗体上 Windows 的网络驱动程序平台的核心基础。 在 NDIS 6.70 在同一时间更新其他网络驱动程序功能的列表，请参阅 Windows 10，版本 1703年部分，了解网络上[什么是驱动程序开发中的新增功能](../what-s-new-in-driver-development.md)。

## <a name="feature-deprecations"></a>功能弃用功能

NDIS 6.70 的版本以及不推荐使用以下网络驱动程序功能：

- [TCP 烟囱卸载](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)
- [IPsec 卸载版本 2](ipsec-offload-version-2.md)

## <a name="implementing-an-ndis-670-driver"></a>实现 NDIS 6.70 驱动程序

### <a name="nic-drivers"></a>NIC 驱动程序

有关实现与 NetAdapterCx NIC 驱动程序的详细信息，请参阅[NetAdapterCx](../netcx/index.md)。

### <a name="miniport-protocol-filter-and-intermediate-drivers"></a>微型端口、 协议、 筛选和中间驱动程序

NDIS 6.70 驱动程序必须遵循在中定义的要求[实现的 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)。

此外，NDIS 6.70 驱动程序必须符合以下要求：

- NDIS 6.70 驱动程序必须报告正确的 NDIS 版本时它会向 NDIS 注册。

   您必须更新的主版本号和次 NDIS 版本编号 NDIS_Xxx_DRIVER_CHARACTERISTICS 结构中以支持 NDIS 6.70。 MajorNdisVersion 成员必须包含 6 和 MinorNdisVersion 成员必须包含 70。 此要求可适用于微型端口、 协议和筛选器驱动程序。 您还必须更新编译器的版本信息 (请参阅[编译的 NDIS 6.70 驱动程序](#compiling-an-ndis-670-driver))。

## <a name="compiling-an-ndis-670-driver"></a>编译 NDIS 6.70 驱动程序

### <a name="nic-drivers"></a>NIC 驱动程序

有关编译 NetAdapterCx NIC 驱动程序的详细信息，请参阅[NetAdapterCx （编译设置） 移植 NDIS 微型端口驱动程序](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md#compilation-settings)。

### <a name="miniport-protocol-and-filter-drivers"></a>微型端口、 协议和筛选器驱动程序

WDK 适用于 Windows 10 版本 1703年支持标头版本控制。 标头版本控制可确保 NDIS 6.70 驱动程序在编译时使用的合适的 NDIS 6.70 数据结构。

将以下编译器设置添加到您的驱动程序的 Visual Studio 项目：

- 微型端口驱动程序，添加```NDIS670_MINIPORT=1```。
- 筛选器或协议驱动程序添加```NDIS670=1```。

有关构建与 Windows 10，版本 1703年版本的 WDK，驱动程序的信息，请参阅[构建一个驱动程序](../develop/building-a-driver.md)。

## <a name="using-ndis-670-driver-data-structures"></a>使用 NDIS 6.70 驱动程序数据结构

### <a name="nic-drivers"></a>NIC 驱动程序

有关 NetAdapterCx 数据结构的详细信息，请参阅[NetAdapterCx](../netcx/index.md)。

### <a name="miniport-protocol-filter-and-intermediate-drivers"></a>微型端口、 协议、 筛选和中间驱动程序

#### <a name="new-data-structures"></a>新的数据结构

以下数据结构是 NDIS 6.70 中的新增功能。

- [NDIS_STATUS_WWAN_DEVICE_CAPS_EX](https://msdn.microsoft.com/library/windows/hardware/mt782396)

