---
title: NDIS 唤醒原因状态指示
description: NDIS 唤醒原因状态指示
ms.assetid: 0229A4F3-8CC1-4A81-9AF4-33BAEBDAE954
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bd5322b1dd532d20f4cc1dca6fa8120c157b2a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544058"
---
# <a name="ndis-wake-reason-status-indications"></a>NDIS 唤醒原因状态指示


从开始 NDIS 6.30，微型端口驱动程序发出 NDIS 唤醒原因状态指示 ([**NDIS\_状态\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh439808)) 到通知 NDIS 和系统唤醒事件的原因有关的基础驱动程序。 如果网络适配器生成唤醒事件时，微型端口驱动程序会立即发出此 NDIS 状态指示系统恢复到全功率状态时。

**请注意**  支持 NDIS 唤醒原因状态指示是可选的移动宽带 (MB) 微型端口驱动程序。

 

本部分包括以下主题：

[NDIS 唤醒原因状态指示的概述](overview-of-ndis-wake-reason-statue-indications.md)

[报告唤醒原因状态指示功能](reporting-wake-reason-status-indication-capabilities.md)

[颁发的 NDIS 唤醒原因状态指示](issuing-ndis-wake-reason-indications.md)

 

 





