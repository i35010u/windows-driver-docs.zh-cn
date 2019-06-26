---
title: 故障转储和休眠支持
description: 故障转储和休眠支持
ms.assetid: 6f5e6f4e-b734-45fe-80d5-fd7b81c9b329
keywords:
- 故障转储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0340bb029588d6094487be86190c5f2c209e3910
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368323"
---
# <a name="crash-dump-and-hibernation-support"></a>故障转储和休眠支持


Storport 虚拟微型端口驱动程序必须支持[ **SCSI\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block) (SRB) 函数代码 SRB\_函数\_转储\_指针。 微型端口驱动程序收到这种类型的 SRB，DataBuffer SRB 成员将指向[**微型端口\_转储\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/ns-storport-_miniport_dump_pointers)结构。 此 SRB 发送到的虚拟微型端口驱动程序，用于控制从微型端口驱动程序返回 SRB 后保存崩溃转储数据磁盘[ **HwStorInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_initialize)例程。

 

 




