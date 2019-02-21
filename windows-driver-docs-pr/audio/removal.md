---
title: HFP 设备删除
description: HFP 设备删除本主题将讨论从 （叶） 删除蓝牙免提配置文件 (HFP) 设备时，会发生什么情况音频系统。
ms.assetid: 99B6C09E-2467-4124-9F9A-5116586BB38C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b13e5dcb722b69a131ebbca0d4439dffef02a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541382"
---
# <a name="hfp-device-removal"></a>HFP 设备删除


HFP 设备删除本主题将讨论从 （叶） 删除蓝牙免提配置文件 (HFP) 设备时，会发生什么情况音频系统。

若要删除配对 HFP 设备，音频驱动程序的已注册的设备接口：

1. 取消任何挂起的 IOCTL\_BTHHFP\_演讲者\_获取\_卷\_状态\_更新 Ioctl。

2. 取消任何挂起的 IOCTL\_BTHHFP\_流\_获取\_状态\_更新 Ioctl。

3. 取消任何挂起的 IOCTL\_BTHHFP\_设备\_获取\_连接\_状态\_更新 Ioctl。

4. 取消引用 HFP 文件对象 （这也取消引用 DeviceObject）。

5. 调用 KsDeleteFilterFactory 删除表示 HFP 设备与已删除接口关联的筛选器工厂。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题
[理论上的操作](theory-of-operation.md)  



