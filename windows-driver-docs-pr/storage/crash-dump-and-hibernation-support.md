---
title: 故障转储和休眠支持
description: 故障转储和休眠支持
ms.assetid: 6f5e6f4e-b734-45fe-80d5-fd7b81c9b329
keywords:
- 故障转储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f27ea665f9427ea98d711719260ead7017b0c40
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185115"
---
# <a name="crash-dump-and-hibernation-support"></a>故障转储和休眠支持


Storport 虚拟微型端口驱动程序必须支持 [**SCSI \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block) (SRB) 函数代码 SRB \_ 函数 \_ 转储 \_ 指针。 当微型端口驱动程序收到此类 SRB 时，DataBuffer SRB 成员指向 [**微型端口 \_ 转储 \_ 指针**](/windows-hardware/drivers/ddi/storport/ns-storport-_miniport_dump_pointers) 结构。 此 SRB 将发送到一个虚拟微型端口驱动程序，该驱动程序用于控制 SRB 从微型端口驱动程序的 [**HwStorInitialize**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize) 例程返回后保存故障转储数据的磁盘。

 

