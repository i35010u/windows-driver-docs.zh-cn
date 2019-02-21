---
title: 故障转储和休眠支持
description: 故障转储和休眠支持
ms.assetid: 6f5e6f4e-b734-45fe-80d5-fd7b81c9b329
keywords:
- 故障转储 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 610511ead89eaf37ccfd68ebdbf2cf29b192402d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547170"
---
# <a name="crash-dump-and-hibernation-support"></a>故障转储和休眠支持


Storport 虚拟微型端口驱动程序必须支持[ **SCSI\_请求\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff565393) (SRB) 函数代码 SRB\_函数\_转储\_指针。 微型端口驱动程序收到这种类型的 SRB，DataBuffer SRB 成员将指向[**微型端口\_转储\_指针**](https://msdn.microsoft.com/library/windows/hardware/ff562247)结构。 此 SRB 发送到的虚拟微型端口驱动程序，用于控制从微型端口驱动程序返回 SRB 后保存崩溃转储数据磁盘[ **HwStorInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff557396)例程。

 

 




