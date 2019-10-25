---
title: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES
description: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES 是一个 TLV，其中包含操作系统电源管理功能的标志。
ms.assetid: 4F104956-1B26-47DF-A58F-53C24B75DB77
ms.date: 03/30/2018
keywords:
- WDI_TLV_OS_POWER_MANAGEMENT_FEATURES 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b5bb2af3ba5af3856fba8ba58f031c29dfa544a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824373"
---
# <a name="wdi_tlv_os_power_management_features"></a>WDI_TLV_OS_POWER_MANAGEMENT_FEATURES

WDI_TLV_OS_POWER_MANAGEMENT_FEATURES 是一个 TLV，其中包含操作系统电源管理功能的标志。 这使 Ihv 能够向操作系统指示它们支持称为 Nic 自动电源保护程序（NAPS）的高级电源管理功能。 NAPS 允许无线适配器在网络活动处于空闲状态的情况下进入*DX* 。

## <a name="tlv-type"></a>TLV 类型

0x144

## <a name="length"></a>长度


以下值的大小（以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_OS_POWER_MANAGEMENT_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_os_power_management_flags) | 定义支持的 NAPS 支持方案的**WDI_OS_POWER_MANAGEMENT_FLAGS**值的按位 or。 |
 

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1803 |
| 最低受支持的服务器 | WIN ENT LTSB 2016 Finnish 64 Bits |
| 标头 | Wditypes.hpp |
