---
title: MB PIN 操作
description: MB PIN 操作
ms.assetid: ca9e1537-29e8-4849-a634-5c2177886321
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d3ce5cc457e997450b662b30e1b6a3b6072e486
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374045"
---
# <a name="mb-pin-operations"></a>MB PIN 操作


本主题介绍与存储在 MB 设备内存中或在用户识别模块 （SIM 卡） 上的订阅信息的访问控制相关的操作。

## <a name="mb-pin-operations-for-device-hibernation"></a>MB 设备休眠状态的固定操作

每个[3GPP](https://www.3gpp.org/about-3gpp)标准，有不同类型的 SIM Pin。  此页上的信息仅适用于 SIM PIN1，也称为通用给定 SIM 卡的 PIN。  

每次从低功耗状态，恢复蜂窝调制解调器 3GPP 标准要求连接到移动电话网络之前刷新 SIM 凭据。  

因为 PC 和基于 Windows 的平板电脑设备断电时系统进入休眠状态时的所有外围设备，SIM 则需要验证，系统将启动时。  

为内部的机箱的调制解调器，Windows 将缓存 SIM PIN 并自动解锁 SIM PIN 时唤醒系统，只要系统进入休眠状态时，调制解调器已解锁。

Windows 通过检测基础的调制解调器设备退出 D3 冷电源状态时执行此操作。  D3 冷是相当于关闭设备电源状态。  

如果移动电话调制解调器设备不支持 D3 冷，Windows 不会自动解锁调制解调器的 SIM PIN。  相反，用户必须手动输入 PIN 以还原移动宽带连接。

有关如何启用 D3 冷 USB 调制解调器设备中的信息，请参阅：

* [USB 设备的支持 D3Cold](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog)。
* [在驱动程序支持 D3cold](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-d3cold-in-a-driver)

有关固定操作的其他信息，请参阅[OID\_WWAN\_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)。
