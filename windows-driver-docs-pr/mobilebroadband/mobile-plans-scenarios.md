---
title: 移动套餐方案
description: 本主题介绍移动运营商可以实现的基本最终用户应用场景。
ms.assetid: 24050B13-4A1A-466F-974B-40B34EDB16DC
keywords:
- Windows Mobile 计划方案, 移动计划实施移动运营商
ms.date: 05/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1a89a4590872b0fa2f856148b6c788cc6ae49179
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948106"
---
# <a name="mobile-plans-scenarios"></a>移动套餐方案

## <a name="overview"></a>概述

本主题提供有关移动运营商将为移动计划启用的最常见方案的指导。 请注意, 这并不是受支持方案的详尽列表。 您可以通过组合使用解决方案来实现您的特定用例。 请咨询你的 Microsoft 联系人以进一步讨论你的需求。

## <a name="install-an-esim-profile-on-a-windows-10-device"></a>在 Windows 10 设备上安装 eSIM 配置文件

本部分介绍了移动运营商在 Windows 10 设备上下载、安装和激活 eSIM 配置文件应采取的步骤。 根据移动运营商的 eSIM 平台和网络后端的 constrainsts, 在激活流程结束时, 有多种方法可用于实现配置文件和网络连接。

1. 开发[移动运营商 web 门户](mobile-plans-web-portal.md#web-portal-interface-for-esim-enabled-devices), 该门户会使用户完成登录和激活步骤。
2. 实现一个受支持的回调方法, 以将控制权返回给移动计划应用, 以下载 eSIM 配置文件:
   1. [内联配置文件下载和连接](mobile-plans-callback-notifications.md#inline-profile-download-and-connectivity)-如果 SM + 服务器已可以发布配置文件, 则应使用此回调方法, 并且该配置文件将使设备在配置文件后立即在手机网络上注册启动. 此方法可将配置文件传递和网络连接作为同一最终用户流的一部分。
   2. [异步连接](mobile-plans-callback-notifications.md#asynchronous-connectivity)。 如果 SM + 服务器已可供释放 eSIM 配置文件, 则应使用此回调方法, 但设备需要等待一段时间, 然后才能尝试注册到移动电话网络。
   3. [配置文件下载延迟](mobile-plans-callback-notifications.md#delayed-esim-profile-download-and-activation)。 当 SM + 服务器无法发布配置文件时, 应使用此回调方法, 并且在一段时间后只能下载此方法。 下载并安装配置文件后, 设备应能够在移动电话网络上注册。
3. 确保正确[处理配置文件下载错误](mobile-plans-eSIM-error-handling.md)。
4. 实现用户的[基本帐户管理体验](mobile-plans-account-management.md#basic-account-management-experience), 以管理和维护其帐户。

## <a name="activate-a-warm-sim-in-a-windows-device"></a>激活 Windows 设备中的热 SIM

本部分介绍允许用户在 Windows 设备中激活热 phsycial SIM 的步骤。 术语 "暖" 指的是已 preactivated 的 SIM, 可以连接到移动运营商网络, 但尚未与活动的订阅相关联。

1. 实现[移动运营商 web 门户](mobile-plans-web-portal.md#web-portal-interface-for-physical-sims), 将引导用户完成登录和激活步骤。
2. 实现回调方法以便[添加余额](mobile-plans-callback-notifications.md#adding-balance)。
3. 实现[增强的帐户管理体验](mobile-plans-account-management.md#enhanced-account-management-experience)。
   1. 将[GetBalance 方法](mobile-plans-account-management.md#getbalance-api)作为移动运营商 API 的一部分实现。
   2. 实现[围墙园](mobile-plans-walled-garden.md), 使用户可以导航到移动运营商 web 门户, 即使他们没有活动余额也是如此。

## <a name="add-balance-to-a-current-subscription"></a>向当前订阅添加余额

本部分介绍添加现有客户订阅余额的步骤 invovled。 当移动运营商销售的预付数据计划必须在平衡运行时表面关闭时, 这非常有用。

1. 开发[移动运营商 web 门户](mobile-plans-web-portal.md)。
2. 实现回调方法以便[添加余额](mobile-plans-callback-notifications.md#adding-balance)。
3. 实现[增强的帐户管理体验](mobile-plans-account-management.md#enhanced-account-management-experience)。
   1. 在移动运营商 API 中实现[GetBalance 方法](mobile-plans-account-management.md#getbalance-api), 以允许在 Windows 网络飞出中显示用户的平衡。
   2. 实现[围墙园](mobile-plans-walled-garden.md), 使用户可以导航到移动运营商 web 门户, 即使他们没有剩余余额也是如此。

## <a name="cancelling-a-transaction"></a>取消事务

本部分介绍在用户浏览移动运营商 web 门户时, 当事务取消时, 用于通知移动计划应用的回调方法。 这适用于本主题中前面的所有方案。

- 实现用于[取消购买流](mobile-plans-callback-notifications.md#canceling-purchase-flow)的回调方法。
