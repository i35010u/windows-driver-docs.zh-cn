---
title: 故障转储和休眠支持
description: 故障转储和休眠支持
keywords:
- 故障转储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c8859d4ea12f060196d69d0c797a15f08ccdf51
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811771"
---
# <a name="crash-dump-and-hibernation-support"></a>故障转储和休眠支持


Storport 虚拟微型端口驱动程序必须支持 [**SCSI \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block) (SRB) 函数代码 SRB \_ 函数 \_ 转储 \_ 指针。 当微型端口驱动程序收到此类 SRB 时，DataBuffer SRB 成员指向 [**微型端口 \_ 转储 \_ 指针**](/windows-hardware/drivers/ddi/storport/ns-storport-_miniport_dump_pointers) 结构。 此 SRB 将发送到一个虚拟微型端口驱动程序，该驱动程序用于控制 SRB 从微型端口驱动程序的 [**HwStorInitialize**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize) 例程返回后保存故障转储数据的磁盘。

 

