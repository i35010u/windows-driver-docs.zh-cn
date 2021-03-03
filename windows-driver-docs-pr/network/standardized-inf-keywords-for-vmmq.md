---
title: VMMQ 的标准化 INF 关键字
description: '* RssOnHostVPorts 标准化 INF 关键字定义为启用或禁用对 VMMQ 的支持。'
ms.date: 02/28/2021
ms.localizationpriority: medium
ms.openlocfilehash: 2c0a44677d21b75ee1709890787059c0ce923634
ms.sourcegitcommit: cf1f4196374c5b743448cb8d688d2223f7197d8f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/03/2021
ms.locfileid: "101751962"
---
# <a name="standardized-inf-keywords-for-vmmq"></a>VMMQ 的标准化 INF 关键字

**\* RSSONHOSTVPORTS** 标准化 INF 关键字定义为启用或禁用对网络适配器虚拟机的支持 [多个队列 (VMMQ)](overview-of-virtual-machine-multiple-queues.md)功能。

**\* RssOnHostVPorts** INF 关键字是一个枚举关键字。 枚举标准化 INF 关键字具有以下属性：

SubkeyName：必须在 INF 文件中指定的关键字的名称。

ParamDesc：与 SubkeyName 关联的显示文本。 

值：与列表中的每个 SubkeyName 相关联的枚举整数值。 

EnumDesc：与菜单中显示的每个值相关联的显示文本。

默认值：菜单的默认值。

下表描述了 **\* RssOnHostVPorts** inf 关键字的可能 inf 条目。

| SubkeyName       | ParamDesc          | “值”       | EnumDesc |
|-------------------|--------------------|-------------|----------|
| \*RssOnHostVPorts | 虚拟交换机 RSS | 0（默认值） | 已禁用 |
|                   |                    | 1           | 已启用  |

在微型端口适配器初始化期间，微型端口驱动程序必须检查 **\* RssOnHostVPorts** 关键字，以确定它是否应在 NIC 上启用 VMMQ 功能。

## <a name="handling-rss-inf-keywords-for-vmmq"></a>处理 VMMQ 的 RSS INF 关键字

如果 NIC 支持 VMMQ，则还应支持 [RSS 的所有标准化 INF 关键字](standardized-inf-keywords-for-rss.md) ，以提供未来的兼容性，即使 OS 当前根本不使用它们。
对于 RSS 功能，应使用普通关键字，但以下情况除外：

-   **\* RSSProfile**：应支持 "ClosestProcessor" 配置文件，并将其用作 VMMQ 的策略。

-   **\* MaxRssProcessors**：当 VMMQ 处于活动状态时，此关键字不应限制在 [**NDIS \_ 接收 \_ 缩放 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)中报告的 .msix 中断消息的数量。