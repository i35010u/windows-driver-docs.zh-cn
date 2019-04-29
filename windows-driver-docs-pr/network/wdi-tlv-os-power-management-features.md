---
title: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES
description: WDI_TLV_OS_POWER_MANAGEMENT_FEATURES 是 TLV，其中包含操作系统电源管理功能的标志。
ms.assetid: 4F104956-1B26-47DF-A58F-53C24B75DB77
ms.date: 03/30/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_OS_POWER_MANAGEMENT_FEATURES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5fdf117dc5ee231a7bf17e2ef2f2e2dd179ceed2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385250"
---
# <a name="wditlvospowermanagementfeatures"></a>WDI_TLV_OS_POWER_MANAGEMENT_FEATURES

WDI_TLV_OS_POWER_MANAGEMENT_FEATURES 是 TLV，其中包含操作系统电源管理功能的标志。 这使得 Ihv 向操作系统指示它们支持名为 Nic 自动 Power 保护程序 (NAPS) 高级的电源管理功能。 NAPS 允许输入的无线适配器*DX*在网络活动处于空闲状态的情况下。

## <a name="tlv-type"></a>TLV 类型

0x144

## <a name="length"></a>长度


以下值的大小 （以字节为单位）。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 描述 |
| --- | --- |
| [**WDI_OS_POWER_MANAGEMENT_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_os_power_management_flags) | 按位 OR **WDI_OS_POWER_MANAGEMENT_FLAGS**支持 NAPS 启用方案定义的值。 |
 

## <a name="requirements"></a>要求

| | |
| --- | --- |
| 最低受支持的客户端 | Windows 10 版本 1803 |
| 最低受支持的服务器 | Windows Server 2016 |
| Header | Wditypes.hpp |
