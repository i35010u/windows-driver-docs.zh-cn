---
title: 确定物理输出的保护级别
description: 确定物理输出的保护级别
ms.assetid: ea06903a-0ad5-43fd-b2d3-013584ae6f69
keywords:
- 保护级别 WDK 显示，确定物理输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efc6ae4e16b771eb4bab21c3c490042a4ff63cec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348826"
---
# <a name="determining-the-protection-level-for-a-physical-output"></a>确定物理输出的保护级别


应使用以下各节中的算法来确定物理的视频输出连接器的保护级别。 在伪代码中表示这些算法。

### <a name="span-idalgorithmforprotectionlevelspanspan-idalgorithmforprotectionlevelspanalgorithm-for-protection-level"></a><span id="algorithm_for_protection_level"></span><span id="ALGORITHM_FOR_PROTECTION_LEVEL"></span>算法的保护级别

应使用以下算法来确定物理的视频输出连接器的保护级别值：

1.  **每个**保护类型 （ACP，CGMS A、 HDCP 和 DPCP） 物理输出连接器支持，请执行以下步骤：
    1.  建议的保护级别设置为无输出保护。 例如，对于的 ACP，驱动程序应保护级别设置为 DXGKMDT\_OPM\_ACP\_关闭; 对于 CGMS A 驱动程序应将保护级别设置为 DXGKMDT\_OPM\_CGMSA\_OFF;为 HDCP，驱动程序应将保护级别设置为 DXGKMDT\_OPM\_HDCP\_OFF; 以及 DPCP，驱动程序应将保护级别设置为 DXGKMDT\_OPM\_DPCP\_关闭。
    2.  **每个**受保护的输出关联物理输出连接器，请执行以下步骤：
        1.  检索当前的保护类型的当前受保护的输出保护级别。
        2.  **如果**当前的保护类型是 CGMS-A，删除 DXGKMDT\_OPM\_重新分发\_控制\_必需标志，如果设置了标志。
        3.  **如果，结束**
        4.  **如果**当前受保护的输出保护级别的优先级高于建议的保护级别，将建议的保护级别设置为当前受保护的输出保护级别。
        5.  **如果，结束**

    3.  **结尾为**
    4.  物理输出保护级别设置为建议的保护级别。

2.  **结尾为**

### <a name="span-idalgorithmforredistributioncontrolspanspan-idalgorithmforredistributioncontrolspanalgorithm-for-redistribution-control"></a><span id="algorithm_for_redistribution_control"></span><span id="ALGORITHM_FOR_REDISTRIBUTION_CONTROL"></span>算法重新分发控件

应使用以下算法来确定物理输出连接器必须启用重新分发控件：

1.  **每个**受保护的输出关联物理输出连接器，请执行以下步骤：
    1.  检索是否设置当前受保护的输出的重新分发控件标记上的信息。
    2.  **如果**DXGKMDT\_OPM\_重新分发\_控制\_必需标志设置，请执行以下步骤：
        1.  启用重新分发控件。
        2.  停止执行算法。

    3.  **如果，结束**

2.  **结尾为**

 

 





