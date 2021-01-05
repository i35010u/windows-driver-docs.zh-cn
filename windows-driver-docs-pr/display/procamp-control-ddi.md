---
title: ProcAmp 控制 DDI
description: ProcAmp 控制 DDI
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2fea01d1d23d8009cda927d96c1e3b6c9b98425e
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812569"
---
# <a name="procamp-control-ddi"></a>ProcAmp 控制 DDI

为了使视频混合呈现器 (VMR) 可以访问 ProcAmp 功能，显示驱动程序必须实现 [运动补偿回调函数](motion-compensation-callbacks.md)。

若要简化驱动程序开发，请使用此部分中的运动补偿代码模板并实现 ProcAmp 控制功能。 函数是取消隔行扫描容器设备或 ProcAmp 控制设备类的成员函数。 有关详细信息，请参阅 [定义隔行扫描容器设备类](./defining-the-deinterlace-container-device-class.md) 和 [定义 ProcAmp Control 设备类](./defining-the-procamp-control-device-class.md)。
