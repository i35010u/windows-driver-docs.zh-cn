---
title: NDIS 6.60 简介
description: 本部分介绍 NDIS 6.60，并介绍了从 NDIS 6.50 的更改。 在 Windows 10，版本 1607年和 Windows Server 2016 和更高版本的 NDIS 6.60。
ms.assetid: AFDFD1CD-2E07-4A4F-82E2-5E6C5AABD5A3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe12b73f1a4db94720a6468cf480407f2449d19d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380598"
---
# <a name="introduction-to-ndis-660"></a>NDIS 6.60 简介

本主题介绍网络驱动程序接口规范 (NDIS) 6.60 并描述其主要设计新增功能。 在 Windows 10，版本 1607年和 Windows Server 2016 和更高版本的 NDIS 6.60。

NDIS 6.60 是次要版本更新到 NDIS 6.50。 有关移植到 NDIS 6.60 NDIS 6.x 驱动程序的详细信息，请参阅[移植 NDIS 6.x 驱动程序到 NDIS 6.60](porting-ndis-6-x-drivers-to-ndis-6-60.md)。

## <a name="feature-updates"></a>功能更新

NDIS 6.60 NDIS 6.50 的增量更新，并且不包含任何主要的新功能。

## <a name="implementing-an-ndis-660-driver"></a>实现 NDIS 6.60 驱动程序

NDIS 6.60 驱动程序必须遵循在中定义的要求[实现的 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)。

此外，NDIS 6.60 驱动程序必须符合以下要求：

- NDIS 6.60 驱动程序必须报告正确的 NDIS 版本时它会向 NDIS 注册。
   
   您必须更新的主版本号和次 NDIS 版本编号 NDIS_Xxx_DRIVER_CHARACTERISTICS 结构中以支持 NDIS 6.60。 MajorNdisVersion 成员必须包含 6 和 MinorNdisVersion 成员必须包含 60。 此要求适用于微型端口、 协议和筛选器驱动程序。 您还必须更新编译器的版本信息 (请参阅[编译的 NDIS 6.60 驱动程序](#compiling-an-ndis-660-driver))。

- Windows 10，版本 1607年和 Windows Server 2016 及更高版本的 NDIS 6.60 微型端口驱动程序必须使用数据结构的 NDIS 6.60 版本。 有关详细信息，请参阅[使用 NDIS 6.60 数据结构](#using-ndis-660-data-structures)。

## <a name="compiling-an-ndis-660-driver"></a>编译 NDIS 6.60 驱动程序

WDK 适用于 Windows 10 版本 1607年支持标头版本控制。 标头版本控制可确保 NDIS 6.60 驱动程序在编译时使用的合适的 NDIS 6.60 数据结构。

将以下编译器设置添加到您的驱动程序的 Visual Studio 项目：

- 微型端口驱动程序，添加```NDIS660_MINIPORT=1```。
- 筛选器或协议驱动程序添加```NDIS660=1```。

有关构建与 Windows 10，版本 1607年版本的 WDK，驱动程序的信息，请参阅[构建一个驱动程序](../develop/building-a-driver.md)。

## <a name="using-ndis-660-data-structures"></a>使用 NDIS 6.60 数据结构

### <a name="updated-data-structures"></a>更新后的数据结构

在 NDIS 6.60 中更新了以下数据结构。

- [NDIS_NIC_SWITCH_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff566583)
- [NDIS_RECEIVE_SCALE_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff567228)
- [NDIS_RECEIVE_SCALE_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff567220)

