---
title: 反交错 DDI
description: 反交错 DDI
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 22c4b018347bf189d6081b05d8a820e86cf869cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809591"
---
# <a name="deinterlace-ddi"></a>反交错 DDI


## <span id="ddk_deinterlace_ddi_gg"></span><span id="DDK_DEINTERLACE_DDI_GG"></span>


为了使视频混合呈现器 (VMR) 可以对视频内容进行逐行转换和执行帧速率转换，显示驱动程序必须实现 [运动补偿回调函数](/windows-hardware/drivers/ddi/index)。

若要简化驱动程序开发，请使用此部分中的运动补偿代码模板并实现取消隔行扫描函数。 函数是取消隔行扫描容器设备或逐行扫描模式设备类的成员函数。 有关详细信息，请参阅 [定义隔行扫描容器设备类](./defining-the-deinterlace-container-device-class.md) 和 [定义隔行扫描 Bob 设备类](./defining-the-deinterlace-bob-device-class.md)。

 

