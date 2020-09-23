---
title: 移动套餐目录
description: 移动套餐目录
ms.assetid: ddc77035-fa0a-4866-b850-aa7926a398ac
keywords:
- Windows Mobile 计划移动运营商
ms.date: 07/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 6796f38cec7f900c1547d839116e4f79deb5bdf8
ms.sourcegitcommit: e6247811ff9a07070547af3d89705dae33a2f465
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "91026424"
---
# <a name="mobile-plans-operator-catalog"></a>Mobile plan 操作员目录

## <a name="overview"></a>概述

使用移动计划应用，用户可以从移动运营商列表中查看和选择。 本文定义了 "选择提供程序" 页面上的移动运营商显示应用的原则。

> [!NOTE]
> "选择提供程序" 页仅适用于已启用 eSIM 的 Windows 10 电脑。 由于旧的物理 UICCs 不允许更改移动运营商的 SIM 配置文件，因此当设备上没有活动 eSIM 时，"选择提供程序" 页将不可用。

![选择提供程序页](images/select_provider_page.png)

## <a name="list-of-mobile-operators"></a>移动运营商列表

- 用户可以查看移动计划中启用的移动运营商列表，以便在给定的国家/地区销售数据计划。
- 设备的物理位置用于确定国家/地区。 当设备通过蜂窝网络连接时，网络 ID 用于确定国家/地区。 如果通过 Wi-fi 连接设备，则国家/地区由反向 IP 决定。
- 向用户显示的移动运营商列表按移动运营商品牌名称的字母顺序进行短路。

## <a name="mobile-operator-branding"></a>移动运营商品牌
- 目录中显示的移动运营商必须使用品牌名称和标记，这些标记通常与他们操作的国家/地区中的手机网络服务相关联。 这是为了让用户清楚地了解服务提供商的身份。
- 移动运营商品牌名称（包括与 Windows PC OEM 关联的品牌元素）将仅向这些 OEM 设备显示。 这是为了防止在不同 OEM 设备上向用户显示 OEM 品牌元素。 移动运营商或 OEM 必须提供设备的品牌和型号 (如 "Windows 系统信息" 对话框中所示，) 的 OEM 品牌移动运营商将在该对话框中提供。

## <a name="device-filtering"></a>设备筛选
- 如果发现设备 (包括调制解调器和/或 eSIM 硬件，或者发现与移动运营商的) firwmare 不兼容的设备，则移动运营商可以请求从该设备上显示的移动操作员列表中进行筛选。 这是为了防止最终用户尝试从无法在其设备上使用的操作员那里获取数据计划。 移动运营商必须提供设备的品牌和型号 (在 Windows 系统信息对话框中找到) 或 eSIM 的 eID，才能启用筛选。
