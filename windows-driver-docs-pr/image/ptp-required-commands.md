---
title: PTP 所需的命令
description: PTP 所需的命令
ms.assetid: 98f4be09-0f13-45a1-b28a-c027e57c0dd7
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7346805e223bc4f4548e4cfe4ee5e7899079711f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534133"
---
# <a name="ptp-required-commands"></a>PTP 所需的命令

PTP 驱动程序必须支持标记为必需中的命令*一致性部分*（第 14 章） PIMA15740 规范。 唯一的例外是**GetNumObjects**不使用命令。

所需的 PTP 命令的完整列表：

0x1001 **GetDeviceInfo**

0x1002 **OpenSession**

0x1003 **CloseSession**

0x1004 **GetStorageIDs**

0x1005 **GetStorageInfo**

0x1007 **GetObjectHandles**

0x1008 **GetObjectInfo**

0x1009 **GetObject**

0x100A **GetThumb**

