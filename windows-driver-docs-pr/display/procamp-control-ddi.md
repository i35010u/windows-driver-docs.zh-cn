---
title: ProcAmp 控制 DDI
description: ProcAmp 控制 DDI
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 473b1d03ee356eca16090776117c05dda2a647a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792959"
---
# <a name="procamp-control-ddi"></a>ProcAmp 控制 DDI


## <span id="ddk_procamp_control_ddi_gg"></span><span id="DDK_PROCAMP_CONTROL_DDI_GG"></span>


为了使视频混合呈现器 (VMR) 可以访问 ProcAmp 功能，显示驱动程序必须实现 [运动补偿回调函数](/windows-hardware/drivers/ddi/index)。

若要简化驱动程序开发，请使用此部分中的运动补偿代码模板并实现 ProcAmp 控制功能。 函数是取消隔行扫描容器设备或 ProcAmp 控制设备类的成员函数。 有关详细信息，请参阅 [定义隔行扫描容器设备类](./defining-the-deinterlace-container-device-class.md) 和 [定义 ProcAmp Control 设备类](./defining-the-procamp-control-device-class.md)。

 

