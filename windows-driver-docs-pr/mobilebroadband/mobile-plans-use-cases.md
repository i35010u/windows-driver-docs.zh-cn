---
title: 移动套餐用例
description: 本主题介绍移动运算符可以实现的基本用户用例。
ms.assetid: 24050B13-4A1A-466F-974B-40B34EDB16DC
keywords:
- Windows Mobile 计划用户情况下，移动计划实现的移动运营商
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8119bb90eb86a6849307020b60cfccab973f0983
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357737"
---
# <a name="mobile-plans-use-cases"></a>移动套餐用例

## <a name="overview"></a>概述

本主题提供有关移动运营商可以让使用计划移动的最常见用例的见解。 请注意，这不受支持的情况下的详尽列表。 很可能，可以通过组合的解决方案实现具体的用例。 请联系您的 Microsoft 联系人讨论更多方案。

## <a name="install-an-esim-profile-on-a-windows-device"></a>在 Windows 设备上安装的 esim 卡配置文件

本部分介绍什么移动运营商应实现以激活、 下载和安装的 Windows 设备上的 esim 卡配置文件。 具体取决于你网络的后端和需要花多长的激活过程的特定条件，您可以实现多个方面将控制返回到计划移动应用。

请执行以下步骤：

1. 实现[计划移动 web 门户](mobile-plans-web-portal.md#web-service-api-used-for-esim)。
2. 实现一种方法让控件返回到计划移动应用。
   1. [内联配置文件传递](mobile-plans-callback-notifications.md#inline-profile-delivery)。 如果 esim 卡配置文件是 SM 中立即可用，则实现此回调的 DP + 服务器和设备可以将附加到移动电话网络立即。
   2. [异步连接](mobile-plans-callback-notifications.md#asynchronous-connectivity)。 如果 esim 卡配置文件是 SM 中立即可用，则实现此回调的 DP + 服务器，但该设备需要等待一段时间之前将附加到移动电话网络。
   3. **异步的配置文件下载**。 如果 esim 卡配置文件是在你 SM 中可用，则实现此回调的 DP + 服务器一段时间和设备后能够立即连接到移动电话网络。
3. [处理 esim 卡下载错误](mobile-plans-eSIM-error-handling.md)。 （可选）
4. 定义[基本的设备体验](mobile-plans-device-experience.md#basic-device-experience)。
5. 提供[计划移动服务配置](mobile-plans-service-configuration.md)信息。
6. [验证](mobile-plans-integration.md)实现。
7. 商业[启动](mobile-plans-launch.md)。

## <a name="add-balance-to-a-current-subscription"></a>将平衡添加到当前订阅

本部分介绍添加到当前订阅的余额所需的工作。 如果您正在销售预付的计划或从 Internet 数据的流失的订阅运行后销售数据的包，这很有用。

1. 实现[移动运营商的 web 门户](mobile-plans-web-portal.md)。
2. 实现[添加平衡](mobile-plans-callback-notifications.md#adding-balance)以将控件返回给移动计划。
3. 实现[增强的设备体验](mobile-plans-device-experience.md#enhanced-device-experience)。
   1. 实现[获取余额 API](mobile-plans-device-experience.md#getbalance-api)。
   2. 实现[围墙花园](mobile-plans-device-experience.md#walled-garden)。
4. 提供[计划移动服务配置](mobile-plans-service-configuration.md)信息。
5. [验证](mobile-plans-integration.md)实现。
6. 商业[启动](mobile-plans-launch.md)。

## <a name="cancelling-a-transaction"></a>正在取消事务

本部分介绍控制回调，以便移动运营商的 web 门户中用户时，事务都会被取消时计划移动应用使用。 这适用于本主题中所有前面的方案。

- 实现[取消购买流](mobile-plans-callback-notifications.md#canceling-purchase-flow)控件。

## <a name="activate-a-warm-sim-in-a-windows-device"></a>激活 Windows 设备中的热 SIM

本部分介绍什么移动运营商应实现来激活 Windows 设备中的热 SIM 配置文件。

请执行以下步骤：

1. 实现[移动运营商的 web 门户](mobile-plans-web-portal.md#web-service-api-used-for-a-physical-sim)。
2. 实现[添加平衡](mobile-plans-callback-notifications.md#adding-balance)以将控件返回给移动计划。
3. 实现[增强的设备体验](mobile-plans-device-experience.md#enhanced-device-experience)。
   1. 实现[获取余额 API](mobile-plans-device-experience.md#getbalance-api)。
   2. 实现[围墙花园](mobile-plans-device-experience.md#walled-garden)。
4. 提供[计划移动服务配置](mobile-plans-service-configuration.md)信息。
5. [验证](mobile-plans-integration.md)实现。
6. 商业[启动](mobile-plans-launch.md)。