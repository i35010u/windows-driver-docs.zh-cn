---
title: 移动计划服务配置
description: 本主题介绍了移动计划程序的配置步骤。
ms.assetid: 95122BBB-0466-4130-9209-7EC6545DFD4D
keywords:
- Windows Mobile 计划配置, 移动计划配置移动运营商
ms.date: 02/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: fe89966e0ea73d60ea20ce7057d495304ce57d7c
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948035"
---
# <a name="mobile-plans-service-configuration"></a>移动计划服务配置

本主题介绍如何在支持移动计划的 Windows 连接设备上构建基础。 其中详细介绍了如何配置 eSIM 配置文件以确保最佳使用者体验, 以及如何提供服务配置信息以确保在 Windows 设备上正确呈现移动计划体验。

## <a name="esim-profile-configuration-requirements"></a>eSIM 配置文件配置要求

您必须准备满足以下要求的 eSIM 配置文件:

- ESIM 配置文件不得锁定 PIN。
- 直到收到配置文件下载已成功完成的确认后, 才能从 SM + 服务器中删除 eSIM 配置文件。 在上一次尝试下载失败时, 可以重新使用激活代码以重试下载相同的配置文件。
- ESIM 配置文件不能设置 "不删除" 或 "不停用" 策略。
- 激活代码不得包含任何前缀, 如 "LPA:"。
- 激活代码立即可用于 MO 直接流。
- 激活代码不得要求 "确认代码"。

### <a name="esim-profile-testing"></a>eSIM 配置文件测试

移动运营商应该执行验证, 以确保可以将其 eSIM 配置文件安装在不同的 Windows 设备上。 为此, 建议为某些可用 eSIM 的设备提供支持, 并使用 Windows 设置应用下载、安装和激活配置文件。

## <a name="service-configuration"></a>服务配置

移动计划服务必须引入一些配置信息以支持移动运营商。 要开始配置过程, 请将电子邮件发送到[移动计划实现支持](mailto:mpimplementation@microsoft.com)。

### <a name="minimum-configuration-information"></a>最小配置信息

1. 要用于产品的品牌名称。
2. 品牌徽标。 所需的解决方法是300x300 像素。 图像还应为完全不透明的出血。
3. 支持解决方案的国家/地区列表。 请使用[ISO 3166 代码](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)创建列表 (以逗号分隔)。
4. MO 直接门户 URI (不支持本地化)。 这应该是*https*地址。 端口号不受支持。
5. 通知 URI。 这是要在其中运行 Javascript 回调 ([回调通知](mobile-plans-callback-notifications.md)) 的主机地址。 这应该是*https*地址。 端口号不受支持。
6. 要与*移动计划*相关联的 ICCID 范围或范围。

下图显示了移动计划应用中 "*标准网关" 页*的示例。 "A" 批注对应于你提交的品牌徽标, "B" 批注对应于品牌名称。

<img src="images/mobile_plans_configuration_mo_page.png" alt="Mobile Plans mobile operator page - asset usage example" title="移动计划移动运营商页面-资产使用情况示例" width="600" />
