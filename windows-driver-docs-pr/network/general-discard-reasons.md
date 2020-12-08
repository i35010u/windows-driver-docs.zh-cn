---
title: 一般性丢弃原因
description: 本部分介绍 Windows 筛选平台标注驱动程序的一般丢弃原因。
keywords:
- 一般丢弃原因网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef5bf27b82aea02c77de0cfea4f0570ec8910007
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825495"
---
# <a name="general-discard-reasons"></a>一般性丢弃原因

筛选器引擎丢弃数据的可能原因的标识符如下所示。 这些标识符是 Fwpstypes 中定义的 FWPS_GENERAL_DISCARD_REASON 枚举中的常量值。

| 丢弃原因标识符 | 丢弃原因说明 |
| --- | --- |
| FWPS_DISCARD_FIREWALL_POLICY | 已从筛选决定返回 FWP_ACTION_BLOCK 操作。 |
| FWPS_DISCARD_IPSEC | 保留。 |

