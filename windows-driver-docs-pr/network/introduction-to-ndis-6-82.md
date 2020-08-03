---
title: NDIS 6.82 简介
description: 本部分介绍了 NDIS 6.82，并介绍了 NDIS 6.81 中的更改。 NDIS 6.82 包含在 Windows 10 版本1809中。
ms.assetid: 6BB75BC5-0E49-4467-B030-E0A23D0ED2DA
ms.date: 08/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: d567e6ceb2e29d53ee968a9a2e1452631b325396
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473755"
---
# <a name="introduction-to-ndis-682"></a>NDIS 6.82 简介

本主题介绍网络驱动程序接口规范（NDIS）6.82，并介绍其主要的设计添加内容。 NDIS 6.82 包含在 Windows 10、版本1809和 Windows Server 2019 及更高版本中。

NDIS 6.82 是 NDIS 6.81 的次要版本更新。 有关将 NDIS 1.x 驱动程序移植到 NDIS 6.82 的详细信息，请参阅[将 ndis 1.x 驱动程序移植到 ndis 6.82](porting-ndis-6-x-drivers-to-ndis-6-82.md)。

## <a name="feature-updates"></a>功能更新

NDIS 6.82 是 NDIS 6.81 的增量更新，不包含任何主要的新功能。

## <a name="implementing-an-ndis-682-driver"></a>实现 NDIS 6.82 驱动程序

NDIS 6.82 驱动程序必须遵循在[实现 NDIS 6.30 驱动程序](implementing-an-ndis-6-30-driver.md)中定义的要求。

此外，NDIS 6.82 驱动程序必须符合以下要求：

- 当 ndis 6.82 驱动程序使用 NDIS 注册时，它必须报告正确的 NDIS 版本。
   
   若要支持 NDIS 6.82，必须在 NDIS_Xxx_DRIVER_CHARACTERISTICS 结构中更新主要和次要 NDIS 版本号。 MajorNdisVersion 成员必须包含6个，并且 MinorNdisVersion 成员必须包含82。 此要求适用于微型端口、协议和筛选器驱动程序。 还必须更新编译器的版本信息（请参阅[编译 NDIS 6.82 驱动程序](#compiling-an-ndis-682-driver)）。

- 适用于 Windows 10、版本1809和 Windows Server 2019 及更高版本的 NDIS 6.82 微型端口驱动程序必须使用 NDIS 6.82 版本的数据结构。

## <a name="compiling-an-ndis-682-driver"></a>编译 NDIS 6.82 驱动程序

适用于 Windows 10 版本1809的 WDK 支持标头版本控制。 标头版本控制可确保 NDIS 6.82 驱动程序在编译时使用合适的 NDIS 6.82 数据结构。

将以下编译器设置添加到你的驱动程序的 Visual Studio 项目中：

- 对于微型端口驱动程序，请添加 `NDIS682_MINIPORT=1` 。
- 对于筛选器或协议驱动程序，请添加 `NDIS682=1` 。

有关使用 Windows 10 1809 版的 WDK 构建驱动程序的信息，请参阅[构建驱动程序](../develop/building-a-driver.md)。
