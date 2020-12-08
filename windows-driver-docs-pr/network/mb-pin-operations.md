---
title: MB PIN 操作
description: MB PIN 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2247a2eb48583f63ccd1d78852f30a5f183b73ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803683"
---
# <a name="mb-pin-operations"></a>MB PIN 操作


本主题介绍与访问控制存储在 MB 设备内存或订阅服务器标识模块 (SIM 卡) 相关的订阅信息的操作。

## <a name="mb-pin-operations-for-device-hibernation"></a>设备休眠的 MB PIN 操作

根据 [3GPP](https://www.3gpp.org/about-3gpp) 标准，有不同类型的 SIM 卡 pin。  本页中的信息仅适用于 SIM PIN1，也称为给定 SIM 卡的通用 PIN。  

每次移动电话调制解调器从低功耗状态恢复时，3GPP 标准要求在连接到移动电话网络之前刷新 SIM 凭据。  

由于 PC 和基于 Windows 的平板电脑在系统进入休眠状态时关闭所有外围设备，因此当系统启动时，需要进行 SIM 验证。  

对于机箱内部的调制解调器，Windows 会缓存 SIM 卡 PIN，并在系统唤醒时自动解锁 SIM 卡，只要系统进入休眠状态，就会解锁调制解调器。

Windows 通过检测基础调制解调器设备何时退出 D3 冷电源状态来实现此功能。  D3 冷指的是与电源关闭等效的设备电源状态。  

如果移动电话调制解调器设备不支持 D3 冷，Windows 不会自动解锁调制解调器的 SIM 卡 PIN。  相反，用户必须手动输入 PIN 才能还原移动宽带连接。

有关如何在 USB 调制解调器设备中启用 D3 冷的信息，请参阅：

* [支持 USB 设备的 D3Cold](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog)。
* [在驱动程序中支持 D3cold](../kernel/supporting-d3cold-in-a-driver.md)

有关 PIN 操作的其他信息，请参阅 [OID \_ WWAN \_ PIN](./oid-wwan-pin.md)。
