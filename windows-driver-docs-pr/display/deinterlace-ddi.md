---
title: 反交错 DDI
description: 反交错 DDI
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f05596d5b89b958ccbddccacd3a4cef4074f5cb5
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812595"
---
# <a name="deinterlace-ddi"></a>反交错 DDI

为了使视频混合呈现器 (VMR) 可以对视频内容进行逐行转换和执行帧速率转换，显示驱动程序必须实现 [运动补偿回调函数](./motion-compensation-callbacks.md)。

若要简化驱动程序开发，请使用此部分中的运动补偿代码模板并实现取消隔行扫描函数。 函数是取消隔行扫描容器设备或逐行扫描模式设备类的成员函数。 有关详细信息，请参阅 [定义隔行扫描容器设备类](./defining-the-deinterlace-container-device-class.md) 和 [定义隔行扫描 Bob 设备类](./defining-the-deinterlace-bob-device-class.md)。
