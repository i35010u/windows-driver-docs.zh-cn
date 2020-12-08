---
title: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES
description: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES 是一种 TLV，其中包含操作系统电源管理功能的标志。
ms.date: 03/30/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_OS_POWER_MANAGEMENT_FEATURES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9ecd6e2cbfa0e65641a583261707fd6f0949a87f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838551"
---
# <a name="wdi_tlv_os_power_management_features"></a>WDI_TLV_OS_POWER_MANAGEMENT_FEATURES

WDI_TLV_OS_POWER_MANAGEMENT_FEATURES 是一种 TLV，其中包含操作系统电源管理功能的标志。 这使 Ihv 能够向操作系统指示它们支持称为 Nic 自动节能功能 (NAPS) 的高级电源管理功能。 NAPS 允许无线适配器在网络活动处于空闲状态的情况下进入 *DX* 。

## <a name="tlv-type"></a>TLV 类型

0x144

## <a name="length"></a>长度


以下值的大小 (以字节为单位) 。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| [**WDI_OS_POWER_MANAGEMENT_FLAGS**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_os_power_management_flags) | 定义支持的 NAPS 支持方案的 **WDI_OS_POWER_MANAGEMENT_FLAGS** 值的按位 or。 |
 

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1803

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp
