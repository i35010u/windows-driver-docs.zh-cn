---
title: PTP 所需命令
description: PTP 所需命令
ms.date: 07/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 19e16c56b2b2246322fe369a16ff04d717419601
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829583"
---
# <a name="ptp-required-commands"></a>PTP 所需命令

PTP 驱动程序必须支持 PIMA15740 规范第14章) 的 "一致性" (*部分* 中标记为 "必需" 的命令。 唯一的例外是，不使用 **GetNumObjects** 命令。

必需的 PTP 命令完整列表为：

0x1001 **GetDeviceInfo**

0x1002 **OpenSession**

0x1003 **CloseSession**

0x1004 **GetStorageIDs**

0x1005 **GetStorageInfo**

0x1007 **GetObjectHandles**

0x1008 相关联 **GetObjectInfo**

0x1009 **GetObject**

0x100A **GetThumb**

