---
title: 示例序列
ms.assetid: 2B15570A-A220-4BF7-B595-D9CF66E02673
keywords:
- 智能卡资源管理器中的 IOCTLs 序列示例，包括启动连接和断开连接
- NFC
- 近场通信
- proximity
- 近场邻近感应
- NFP
description: 提供智能卡资源管理器中 IOCTLs 序列的示例，包括启动、连接和断开连接。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fff748d7c696c5c0abf46e539a65c92aca542d89
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843414"
---
# <a name="example-sequence"></a>示例序列


下面是智能卡资源管理器中 IOCTLs 的一个示例序列：

## <a name="start-up-sequence"></a>启动序列


1.  使用具有智能卡访问设备接口 GUID 的 DevObj 或 Cfgmgr.lnk API 来发现 NFC 设备驱动程序的名称，并将其与 CreateFile 一起使用以打开设备句柄。

2.  初始化线程池。

3.  确定读取器名称。

    -   IOCTL\_智能卡\_在放弃\_ATTR 上获取\_特性\_供应商\_名称、放弃\_属性\_供应商\_IFD\_类型和放弃\_ATTR\_设备\_单元

4.  确定读取器特征。
    -   IOCTL\_智能卡\_在\_放弃上获取\_特性\_特性

5.  启动卡状态监视器。
    -   IOCTL\_智能卡\_\_存在–等待智能卡到达。

    -   IOCTL\_智能卡\_\_不存在–等待智能卡离开。

因为我们不支持放弃\_吞并，放弃\_通电状态，所以重置功能是不相关的。

## <a name="connect-sequence"></a>连接顺序


1.  循环起点。

2.  IOCTL\_智能卡\_获取\_状态

    -   大小写放弃\_未知和放弃\_不存在，不执行任何操作

    -   Case 放弃\_存在，吞并卡

    -   Case 放弃\_吞并，冷重置

    -   放弃\_电源、热重置

    -   Case 放弃\_流通，确定卡 ATR

    -   Case 放弃\_特定的，确定卡 ATR 和协议

3.  IOCTL\_智能卡\_集\_协议

## <a name="disconnect-sequence"></a>断开连接序列


1.  关机超时。

2.  循环起点。

3.  IOCTL\_智能卡\_获取\_状态

    -   案例放弃\_特定、放弃\_流通、放弃\_已接通电源，并将电源关闭

    -   Case 放弃\_吞并，放弃\_存在，不执行任何操作

    -   Case 放弃\_不存在，放弃\_未知，不执行任何操作

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口（DDI）概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[智能卡 DDI 和命令参考](https://docs.microsoft.com/previous-versions/dn905601(v=vs.85))  
