---
title: SetupAPI 日志中的驱动程序分级信息
description: SetupAPI 日志中的驱动程序分级信息
keywords:
- Setupapi.log 日志记录 WDK Windows Vista，驱动程序排名信息
- 签名指示器 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a13392dd7fb5b5604f89187b53b51c696932ec17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782719"
---
# <a name="driver-rank-information-in-the-setupapi-log"></a>SetupAPI 日志中的驱动程序分级信息


Windows 使用签名指示器来表示签名类型。 Windows 将此信息保存在 [驱动程序存储区](driver-store.md) 数据库中供内部使用。

当 Windows 安装驱动程序时，Setupapi.log 会添加一个 *排名* 条目，该条目将以十六进制格式记录驱动程序排名和记录签名类型的签名者评分条目。 下面是一个 Setupapi.log 设备日志的摘录，该日志以粗体字显示，其中显示了一个排名条目示例和一个签名人评分条目示例。 在此摘录中，排名条目指示驱动程序的排名为 "0x0dff0000"，而签名者评分条目表示该驱动程序是收件箱驱动程序。

```cpp
     dvi:      Created Driver Node:
     dvi:           HardwareID   - ROOT\UPDATE
     dvi:           InfName      - D:\Windows\System32\DriverStore\FileRepository\machine.inf_36c3d8da\machine.inf
     dvi:           DevDesc      - Microcode Update Device
     dvi:           DrvDesc      - Microcode Update Device
     dvi:           Provider     - Microsoft
     dvi:           Mfg          - (Standard system devices)
     dvi:           InstallSec   - UPDATE_DRV
     dvi:           ActualSec    - UPDATE_DRV
     dvi:           Rank         - 0x0dff0000
     dvi:           Signer       - Microsoft Windows Component Publisher
     dvi:           Signer Score - INBOX
     dvi:           DrvDate      - 10/01/2002
     dvi:           Version      - 6.0.5270.8
```

以下是 Windows 在 Setupapi.log 设备日志中为每种类型的签名记录的签名者评分条目列表：

<a href="" id="premium-whql-signature"></a>高级 WHQL 签名  
"签署人评分-WHQL 徽标黄金"

<a href="" id="standard-whql-signature"></a>标准 WHQL 签名  
"签署人评分-WHQL 徽标银"

<a href="" id="an-unspecified-microsoft-signature"></a>未指定的 Microsoft 签名  
"签署人评分-WHQL 未分类"

<a href="" id="a-whql-signature-for-a-windows-version-earlier-than-windows-vista-and-equal-to-or-later-than-the-lowerlogoversion-value-of-the-driver-s-device-setup-class-"></a>早于 Windows Vista 的 Windows 版本的 WHQL 签名，并且等于或晚于驱动程序的设备安装程序类的 [LowerLogoVersion](lowerlogoversion.md) 值。  
"签署人评分-WHQL"

<a href="" id="a-microsoft-signature-for-an-inbox-driver"></a>收件箱驱动程序的 Microsoft 签名  
"签署人评分-收件箱"

<a href="" id="an-authenticode-signature-or-whql-signature-for-a-windows-version-earlier-than-the-version-that-is-specified-by-lowerlogoversion-for-the-device-setup-class-of-the-driver"></a>早于 **LowerLogoVersion** 为驱动程序的设备安装程序类指定的版本的 Windows 版本的 Authenticode 签名或 WHQL 签名  
"签署人评分-Authenticode"

<a href="" id="unsigned-driver"></a>未签名驱动程序  
"签署人评分-未经过数字签名"

有关驱动程序排名的详细信息，请参阅 [windows (Windows Vista 和更高版本) 的驱动程序的方式 ](how-setup-ranks-drivers--windows-vista-and-later-.md)。

 

 





