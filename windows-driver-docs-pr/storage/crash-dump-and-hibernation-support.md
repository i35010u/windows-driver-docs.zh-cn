---
title: 故障转储和休眠支持
description: 故障转储和休眠支持
ms.assetid: 6f5e6f4e-b734-45fe-80d5-fd7b81c9b329
keywords:
- 故障转储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8f0aacf4662847cdb5038832dfa0c8738f58513
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844574"
---
# <a name="crash-dump-and-hibernation-support"></a>故障转储和休眠支持


Storport 虚拟微型端口驱动程序必须支持[**SCSI\_请求\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)（SRB）函数代码 SRB\_函数\_转储\_指针。 当微型端口驱动程序收到此类型的 SRB 时，DataBuffer SRB 成员指向[**微型端口\_转储\_指针**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/ns-storport-_miniport_dump_pointers)结构。 此 SRB 将发送到一个虚拟微型端口驱动程序，该驱动程序用于控制 SRB 从微型端口驱动程序的[**HwStorInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)例程返回后保存故障转储数据的磁盘。

 

 




