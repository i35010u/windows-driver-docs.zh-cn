---
title: 示例序列
ms.assetid: 2B15570A-A220-4BF7-B595-D9CF66E02673
keywords:
- Ioctl 序列中包括启动连接和断开连接的智能卡资源管理器的示例
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: 提供在智能卡资源管理器，包括启动、 连接和断开连接的 Ioctl 序列的示例。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7d1f41aa55de7081873932d581dc6532a060c37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566874"
---
# <a name="example-sequence"></a>示例序列


下面是 Ioctl 智能卡资源管理器中的示例序列：

## <a name="start-up-sequence"></a>启动顺序


1.  使用智能卡访问设备接口的 GUID 与 DevObj 或 CfgMgr API，以发现 NFC 设备驱动程序的名称，并将其用于 CreateFile 打开的设备句柄。

2.  初始化线程池。

3.  确定读取器的名称。

    -   IOCTL\_智能卡\_获取\_放弃属性\_ATTR\_供应商\_名称、 放弃\_ATTR\_供应商\_IFD\_类型并放弃\_ATTR\_设备\_单元

4.  确定读取器的特征。
    -   IOCTL\_智能卡\_获取\_放弃属性\_ATTR\_特征

5.  启动卡状态监视器。
    -   IOCTL\_智能卡\_IS\_存在 – 要等待的时间智能卡到达。

    -   IOCTL\_智能卡\_IS\_ABSENT – 要等待的时间智能卡出发。

重置电源是不相关，因为我们不支持放弃\_SWALLOWED、 放弃\_提供支持的状态。

## <a name="connect-sequence"></a>连接序列


1.  循环的开头。

2.  IOCTL\_智能卡\_获取\_状态

    -   本例中放弃\_UNKNOWN 和放弃\_不存在，不执行任何操作

    -   本例中放弃\_存在，允许存在卡

    -   本例中放弃\_被抑制，冷重置

    -   本例中放弃\_提供支持，尝试重置

    -   本例中放弃\_NEGOTIABLE，确定卡 ATR

    -   本例中放弃\_特定，确定卡 ATR 和协议

3.  IOCTL\_智能卡\_设置\_协议

## <a name="disconnect-sequence"></a>断开连接序列


1.  启动电源关闭超时。

2.  循环的开头。

3.  IOCTL\_智能卡\_获取\_状态

    -   本例中放弃\_详细信息，放弃\_NEGOTIABLE、 放弃\_提供支持，将幂设置向下

    -   本例中放弃\_SWALLOWED、 放弃\_存在，不执行任何操作

    -   本例中放弃\_不存在，放弃\_未知、 不执行任何操作

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[智能卡 DDI 和命令参考](https://msdn.microsoft.com/library/windows/hardware/dn905601)  
