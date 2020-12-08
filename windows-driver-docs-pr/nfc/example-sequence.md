---
title: 示例序列
keywords:
- 智能卡资源管理器中的 IOCTLs 序列示例，包括启动连接和断开连接
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
description: 提供智能卡资源管理器中 IOCTLs 序列的示例，包括启动、连接和断开连接。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51875b06c9b939d108ba7b181fc776c7f4b6da79
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813589"
---
# <a name="example-sequence"></a>示例序列


下面是智能卡资源管理器中 IOCTLs 的一个示例序列：

## <a name="start-up-sequence"></a>启动序列


1.  使用具有智能卡访问设备接口 GUID 的 DevObj 或 Cfgmgr.lnk API 来发现 NFC 设备驱动程序的名称，并将其与 CreateFile 一起使用以打开设备句柄。

2.  初始化线程池。

3.  确定读取器名称。

    -   IOCTL \_ 智能卡 \_ 获取 \_ 放弃属性 \_ \_ 供应商 \_ 名称、放弃属性 \_ \_ 供应商 \_ IFD \_ 类型和放弃 \_ attr \_ 设备 \_ 的属性

4.  确定读取器特征。
    -   IOCTL \_ 智能卡 \_ 获取 \_ 放弃属性 \_ \_ 特征的属性

5.  启动卡状态监视器。
    -   \_存在 IOCTL \_ 智能 \_ 卡–等待智能卡到达。

    -   \_缺少 IOCTL \_ 智能 \_ 卡–等待智能卡离开。

因为我们不支持放弃 \_ 吞并，放弃供电状态，所以重置功能是不相关的 \_ 。

## <a name="connect-sequence"></a>连接顺序


1.  循环起点。

2.  IOCTL \_ 智能卡 \_ 获取 \_ 状态

    -   Case 放弃 \_ UNKNOWN 和放弃 \_ 不存在，不执行任何操作

    -   Case 放弃 \_ ，吞并卡

    -   Case 放弃 \_ 吞并，冷重置

    -   放弃 \_ 电源、热重置的情况

    -   Case 放弃 \_ 流通，确定卡 ATR

    -   放弃特定情况下 \_ ，确定卡 ATR 和协议

3.  IOCTL \_ 智能卡 \_ 设置 \_ 协议

## <a name="disconnect-sequence"></a>断开连接序列


1.  关机超时。

2.  循环起点。

3.  IOCTL \_ 智能卡 \_ 获取 \_ 状态

    -   案例放弃 \_ 特定，放弃 \_ 流通，放弃， \_ 设置电源关闭

    -   Case 放弃 \_ 吞并，放弃 \_ 存在，不执行任何操作

    -   Case 放弃 \_ 不存在，放弃 \_ 未知，不执行任何操作

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/index)  
[智能卡 DDI 和命令参考](/previous-versions/dn905601(v=vs.85))
