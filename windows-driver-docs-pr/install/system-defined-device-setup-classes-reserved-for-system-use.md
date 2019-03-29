---
title: 保留给系统使用的系统定义的设备安装程序类
description: 保留给系统使用的系统定义的设备安装程序类
ms.assetid: 519a8833-8ed0-40c8-b7cb-a86f13191227
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e43522a6366e6e5bde454e778e371b6dc14fc48f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575284"
---
# <a name="system-defined-device-setup-classes-reserved-for-system-use"></a>保留给系统使用的系统定义的设备安装程序类


下面的类和 Guid 不应安装设备 （或驱动程序） 在 Windows 2000 或更高版本的 Windows 上：

**适配器**<br/>
类 = 适配器<br/>
ClassGuid = {4d36e964-e325-11ce-bfc1-08002be10318}<br/>
此类已过时。

**APM**<br/>
类 = APMSupport<br/>
ClassGuid = {d45b1c18-c8fa-11d1-9f77-0000f805f530}<br/>
此类保留供系统使用。

<a href="" id="computer-"></a>**计算机**<br/>
类 = 计算机<br/>
ClassGuid = {4d36e966-e325-11ce-bfc1-08002be10318}<br/>
此类保留供系统使用。

<a href="" id="decoders-"></a>**解码器**<br/>
类 = 解码器<br/>
ClassGuid = {6bdd1fc2-810f-11d0-bec7-08002be2092f}<br/>
此类保留供将来使用。

**主机端 IEEE 1394 内核调试程序支持**<br/>
类 = 1394Debug<br/>
ClassGuid = {66f250d6-7801-4a64-b139-eea80a450b24}<br/>
此类保留供系统使用。

**IEEE 1394 IP 网络枚举器**<br/>
类 = Enum1394<br/>
ClassGuid = {c459df55-db08-11d1-b009-00a0c9081ff6}<br/>
此类保留供系统使用。

**没有驱动程序**<br/>
类 = NoDriver<br/>
ClassGuid = {4d36e976-e325-11ce-bfc1-08002be10318}<br/>
此类已过时。

<a href="" id="non-plug-and-play-drivers-"></a>**非即插驱动程序**<br/>
类 = LegacyDriver<br/>
ClassGuid = {8ecc055d-047f-11d1-a537-0000f8753ed1}<br/>
此类保留供系统使用。

<a href="" id="other-devices-"></a>**其他设备**<br/>
类 = 未知<br/>
ClassGuid = {4d36e97e-e325-11ce-bfc1-08002be10318}<br/>
此类保留供系统使用。 此类安装枚举的系统不能为其确定类型的设备。 不要使用此类不确定你的设备所属的类中。 确定正确的设备安装程序类，或者创建一个新类。

<a href="" id="printer-upgrade-"></a>**打印机升级**<br/>
类 = PrinterUpgrade<br/>
ClassGuid = {4d36e97a-e325-11ce-bfc1-08002be10318}<br/>
此类保留供系统使用。

<a href="" id="sound-"></a>**声音**<br/>
类 = 声音<br/>
ClassGuid = {4d36e97c-e325-11ce-bfc1-08002be10318}<br/>
此类已过时。

**存储卷的快照**<br/>
类 = VolumeSnapshot<br/>
ClassGuid = {533c5b84-ec70-11d2-9505-00c04F79deaf}<br/>
此类保留供系统使用。

**USB 总线设备 （中心和主机控制器）**<br/>
类 = USB<br/>
ClassGuid = {36fc9e60-c465-11cf-8056-444553540000}<br/>
此类包括 USB 主控制器和 USB 集线器，但不是 USB 外围设备。 此类的驱动程序是系统提供。

 

 





