---
title: SCSI 端口驱动程序支持例程
description: 介绍 SCSI 端口驱动程序例程。
keywords:
- SCSI 端口驱动程序支持例程
- 存储 WDK
- 存储支持例程
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 936fde8f810b7d36fe082876db8cac3e305dc69d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839409"
---
# <a name="scsi-port-driver-support-routines"></a>SCSI 端口驱动程序支持例程

特定于操作系统的 SCSI 端口驱动程序提供 *ScsiPortXxx* 例程，以支持与 Microsoft 提供的、特定于操作系统的 scsi 端口驱动程序关联的独立于操作系统的 scsi 微型端口驱动程序。 SCSI 端口驱动程序是一个内核模式的动态链接库。

可在以下位置找到 *ScsiPortXxx* 例程的列表和引用页：

| 例程 | 标头 |
| ------- | ------- |
| *ScsiPortXxx* | [srb 标头](/windows-hardware/drivers/ddi/srb/) |
| *ScsiPortWmiXxx* | [scsiwmi](/windows-hardware/drivers/ddi/scsiwmi/) |

有关 SCSI 微型端口驱动程序例程的列表，请参阅 [Scsi 微型端口驱动程序例程](scsi-miniport-driver-routines.md)。
