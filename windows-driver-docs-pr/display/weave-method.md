---
title: Weave 方法
description: Weave 方法
keywords:
- DirectX VPE 支持 WDK DirectDraw，并显示隔行扫描视频
- 绘制 VPEs WDK DirectDraw 并显示交错视频
- DirectDraw VPEs WDK Windows 2000 显示，显示交错视频
- 视频端口扩展 WDK DirectDraw，显示交错视频
- VPEs WDK DirectDraw，显示交错视频
- 显示隔行扫描视频
- 交错视频显示 WDK 视频端口扩展
- 编织 WDK DirectDraw
- 取消隔行扫描 WDK 视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26667a1d6e0b7f3296b1efd4c13719e07ed972e2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786345"
---
# <a name="weave-method"></a>Weave 方法


## <span id="ddk_weave_method_gg"></span><span id="DDK_WEAVE_METHOD_GG"></span>


编织方法使用硬件视频端口显示数据，以将交错字段交错到覆盖曲面中，然后同时显示这两个字段。 不过，如果这是所有的编织算法，则会显示运动项目。 "编织" 算法还依赖于 MPEG 驱动程序来识别3:2 模式，然后使用内核模式视频传输中的函数对其进行撤消。 内核模式视频传输可能导致硬件视频端口丢弃重复的字段，从而导致所有字段对来自同一帧。 结果为每秒24帧显示的全帧视频，就像最初使用胶片进行采样一样。

每个源胶卷帧在 NTSC 信号中用两个或三个字段表示。 这可以查看构成帧的两个字段。 四个胶片帧的每个序列都转换为五个电视帧。 胶片帧 A、B、C 和 D 变成了具有字段模式 AA、BB、BC、CD 和 DD 的五个电视帧。 当使用 "重复 \_ 字段" 标志在 MPEG 流中对此模式进行编码时，mpeg 数据有效负载仅包含四个帧，但会保留所有五个电视帧的字段顺序。

编织方法每秒产生24个渐进帧，并保留来自交错源的完整垂直分辨率。 如果视频是使用3:2 下拉的电影创建的，或者，如果它不包含任何运动，则编织是渐进式监视器的最佳显示效果。

 

 





