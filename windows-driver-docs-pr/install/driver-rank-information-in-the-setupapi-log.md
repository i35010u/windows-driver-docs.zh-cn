---
title: SetupAPI 日志中的驱动程序分级信息
description: SetupAPI 日志中的驱动程序分级信息
ms.assetid: 169a1963-3fb3-4254-9634-78034cda2924
keywords:
- SetupAPI 日志记录 WDK Windows Vista 中，驱动程序排名的信息
- 签名指示器 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88a0583922123f50ba3b33c08e5f01eb5fe62402
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356020"
---
# <a name="driver-rank-information-in-the-setupapi-log"></a>SetupAPI 日志中的驱动程序分级信息


Windows 使用签名指示器来表示签名类型。 Windows 将在此信息保存[驱动程序存储区](driver-store.md)供内部使用的数据库。

当 Windows 安装的驱动程序时，将添加 SetupAPI*排名*十六进制格式和记录签名类型的签名者分数条目中记录驱动程序级别的条目。 以下是粗体的字体样式、 排名条目示例和签名者分数条目的示例中所示，SetupAPI 设备日志的摘录。 在此摘录中，排名条目指示驱动程序的"0x0dff0000"的排名和签名者分数条目指示驱动程序将收件箱驱动程序。

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

以下是签名的 Windows 中每种类型 SetupAPI 设备日志的日志签名者分数条目的列表：

<a href="" id="premium-whql-signature"></a>高级 WHQL 签名  
"签名者 Score-WHQL 徽标金牌"

<a href="" id="standard-whql-signature"></a>标准 WHQL 签名  
"签名者 Score-WHQL 徽标 Silver"

<a href="" id="an-unspecified-microsoft-signature"></a>未指定的 Microsoft 签名  
"签名者 Score-WHQL 未分类"

<a href="" id="a-whql-signature-for-a-windows-version-earlier-than-windows-vista-and-equal-to-or-later-than-the-lowerlogoversion-value-of-the-driver-s-device-setup-class-"></a>Windows 版本早于 Windows Vista 且等于或晚于 WHQL 签名[LowerLogoVersion](lowerlogoversion.md)驱动程序的设备安装程序类的值。  
"签名者 Score-WHQL"

<a href="" id="a-microsoft-signature-for-an-inbox-driver"></a>用于收件箱驱动程序的 Microsoft 签名  
"签名者 Score 的收件箱"

<a href="" id="an-authenticode-signature-or-whql-signature-for-a-windows-version-earlier-than-the-version-that-is-specified-by-lowerlogoversion-for-the-device-setup-class-of-the-driver"></a>Authenticode 签名或早于由指定的版本的 Windows 版本的 WHQL 签名**LowerLogoVersion**设备安装程序类的驱动程序  
"签名者 Score 的验证码"

<a href="" id="unsigned-driver"></a>未签名驱动程序  
"签名者 Score-未经过数字签名"

有关驱动程序分级的详细信息，请参阅[如何 Windows Ranks Drivers （Windows Vista 和更高版本）](how-setup-ranks-drivers--windows-vista-and-later-.md)。

 

 





