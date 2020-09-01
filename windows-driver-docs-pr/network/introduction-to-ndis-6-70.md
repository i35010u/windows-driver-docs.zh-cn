---
title: NDIS 6.70 简介
description: 本部分介绍了 NDIS 6.70，并介绍了 NDIS 6.60 中的更改。 NDIS 6.70 包含在 Windows 10 版本1703中。
ms.assetid: D846EE68-2C84-40E0-91DE-2034F75D576F
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97d75f2f2c8f382d880a186a0aab3be54eca52ac
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206417"
---
# <a name="introduction-to-ndis-670"></a>NDIS 6.70 简介

本主题介绍 (NDIS) 6.70 的网络驱动程序接口规范，并介绍了其主要的设计添加。 NDIS 6.70 包含在 Windows 10 版本1703中。

对于微型端口、协议、筛选器和中间驱动程序，NDIS 6.70 是 NDIS 6.60 的次要版本更新。 有关将 NDIS 1.x 驱动程序移植到 NDIS 6.70 的详细信息，请参阅 [将 ndis 1.x 驱动程序移植到 ndis 6.70](porting-ndis-6-x-drivers-to-ndis-6-70.md)。

## <a name="feature-updates"></a>功能更新

### <a name="netadaptercx"></a>NetAdapterCx

除了 NDIS 6.70，Windows 10、版本1703，还包括称为网络适配器 WDF 类扩展的 NIC 驱动程序的主要新功能，也称为 [NetAdapterCx](../netcx/index.md)。 NetAdapterCx 仅在 Windows 10 版本1703中处于预览阶段。 NetAdapterCx 模型使 NIC 驱动程序开发人员能够充分利用 WDF 的全部功能和简化驱动程序模型，这意味着 NIC 驱动程序更易于编写。

### <a name="other-feature-updates"></a>其他功能更新

NDIS 形成 Windows 上网络驱动程序平台的核心基础。 有关与 NDIS 6.70 同时更新的其他网络驱动程序功能的列表，请参阅 Windows 10 版本1703部分，了解 [驱动程序开发中的新增](../what-s-new-in-driver-development.md)功能。

## <a name="feature-deprecations"></a>功能弃用功能

以下网络驱动程序功能已弃用，并且已发布 NDIS 6.70：

- [TCP 烟囱卸载](/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)
- [IPsec 卸载版本 2](./introduction-to-ipsec-offload-version-2.md)

## <a name="implementing-an-ndis-670-driver"></a>实现 NDIS 6.70 驱动程序

### <a name="nic-drivers"></a>NIC 驱动程序

有关使用 NetAdapterCx 实现 NIC 驱动程序的详细信息，请参阅 [NetAdapterCx](../netcx/index.md)。

### <a name="miniport-protocol-filter-and-intermediate-drivers"></a>微型端口、协议、筛选器和中间驱动程序

NDIS 6.70 驱动程序必须遵循在 [实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中定义的要求。

此外，NDIS 6.70 驱动程序必须符合以下要求：

- 当 ndis 6.70 驱动程序使用 NDIS 注册时，它必须报告正确的 NDIS 版本。

   若要支持 NDIS 6.70，必须在 NDIS_Xxx_DRIVER_CHARACTERISTICS 结构中更新主要和次要 NDIS 版本号。 MajorNdisVersion 成员必须包含6个，并且 MinorNdisVersion 成员必须包含70。 此要求适用于微型端口、协议和筛选器驱动程序。 还必须更新编译器的版本信息 (参阅 [编译 NDIS 6.70 驱动程序](#compiling-an-ndis-670-driver)) 。

## <a name="compiling-an-ndis-670-driver"></a>编译 NDIS 6.70 驱动程序

### <a name="nic-drivers"></a>NIC 驱动程序

有关使用 NetAdapterCx 编译 NIC 驱动程序的详细信息，请参阅 [将 NDIS 微型端口驱动程序移植到 NetAdapterCx (编译设置) ](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md#compilation-settings)。

### <a name="miniport-protocol-and-filter-drivers"></a>微型端口、协议和筛选器驱动程序

适用于 Windows 10 版本1703的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.70 驱动程序在编译时使用合适的 NDIS 6.70 数据结构。

将以下编译器设置添加到你的驱动程序的 Visual Studio 项目中：

- 对于微型端口驱动程序，请添加 ```NDIS670_MINIPORT=1``` 。
- 对于筛选器或协议驱动程序，请添加 ```NDIS670=1``` 。

有关使用 Windows 10 1703 版的 WDK 构建驱动程序的信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

## <a name="using-ndis-670-driver-data-structures"></a>使用 NDIS 6.70 驱动程序数据结构

### <a name="nic-drivers"></a>NIC 驱动程序

有关 NetAdapterCx 数据结构的详细信息，请参阅 [NetAdapterCx](../netcx/index.md)。

### <a name="miniport-protocol-filter-and-intermediate-drivers"></a>微型端口、协议、筛选器和中间驱动程序

#### <a name="new-data-structures"></a>新数据结构

以下数据结构是在 NDIS 6.70 中新增的。

- [NDIS_STATUS_WWAN_DEVICE_CAPS_EX](./ndis-status-wwan-device-caps-ex.md)