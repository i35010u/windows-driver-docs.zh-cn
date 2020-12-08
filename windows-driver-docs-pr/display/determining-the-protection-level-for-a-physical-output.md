---
title: 确定物理输出的保护级别
description: 确定物理输出的保护级别
keywords:
- 显示的保护级别，为物理输出确定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ebe1a6aac7eeac4ae7b9ba52b3947159bff027f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809517"
---
# <a name="determining-the-protection-level-for-a-physical-output"></a>确定物理输出的保护级别


应使用以下部分中的算法来确定物理视频输出连接器的保护级别。 这些算法以伪代码形式表示。

### <a name="span-idalgorithm_for_protection_levelspanspan-idalgorithm_for_protection_levelspanalgorithm-for-protection-level"></a><span id="algorithm_for_protection_level"></span><span id="ALGORITHM_FOR_PROTECTION_LEVEL"></span>保护级别的算法

应使用以下算法来确定物理视频输出连接器的保护级别值：

1.  **对于每种** 保护类型 (，物理输出连接器支持的 ACP、CGMS、HDCP 和 DPCP) ，请执行以下步骤：
    1.  将建议的保护级别设置为 "无输出保护"。 例如，对于 ACP，驱动程序应将保护级别设置为 DXGKMDT \_ OPM \_ ACP \_ OFF; 对于 CGMS，驱动程序应将保护级别设置为 DXGKMDT \_ OPM \_ CGMSA \_ off; 对于 HDCP，驱动程序应将保护级别设置为 "DXGKMDT \_ OPM hdcp" \_ ; 对于 \_ DPCP，驱动程序应将保护级别设置为 "DXGKMDT \_ OPM \_ DPCP off" \_ 。
    2.  对于与物理输出连接器关联的 **每个** 受保护的输出，请执行以下步骤：
        1.  为当前保护类型检索当前受保护的输出保护级别。
        2.  **如果** 当前保护类型为 CGMS，则在设置了标志的情况下删除 DXGKMDT \_ OPM \_ 再分发 \_ 控制 \_ 必需标志。
        3.  **结束 if**
        4.  **如果** 当前受保护的输出的保护级别高于建议的保护级别，请将建议的保护级别设置为当前受保护的输出保护级别。
        5.  **结束 if**

    3.  **结束**
    4.  将物理输出的保护级别设置为建议的保护级别。

2.  **结束**

### <a name="span-idalgorithm_for_redistribution_controlspanspan-idalgorithm_for_redistribution_controlspanalgorithm-for-redistribution-control"></a><span id="algorithm_for_redistribution_control"></span><span id="ALGORITHM_FOR_REDISTRIBUTION_CONTROL"></span>用于再分发控制的算法

应使用以下算法来确定物理输出连接器是否必须启用再发行控制：

1.  对于与物理输出连接器关联的 **每个** 受保护的输出，请执行以下步骤：
    1.  检索有关当前受保护的输出的再发行控制标志是否已设置的信息。
    2.  **如果** \_ \_ 已设置 DXGKMDT OPM 再分发 \_ 控制 \_ 必需标志，请执行以下步骤：
        1.  启用再分发控制。
        2.  停止执行该算法。

    3.  **结束 if**

2.  **结束**

 

 





