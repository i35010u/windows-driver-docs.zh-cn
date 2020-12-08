---
title: 微型驱动程序 INI 文件中的 BidiFiles 项
description: 微型驱动程序 INI 文件中的 BidiFiles 项
keywords:
- BidiFiles 部分
- INF 文件 WDK 打印，双向扩展文件信息
- 双向扩展文件 WDK 打印机自动配置
- 内置自动配置支持 WDK 打印机，双向扩展文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2700ffdaae2e95ee8ffb242bc08716c8fb554d84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797813"
---
# <a name="bidifiles-entry-in-a-minidrivers-ini-file"></a>微型驱动程序 INI 文件中的 BidiFiles 项


打印机微型驱动程序通过特定于微型驱动程序的 INI 文件向端口监视器传达有关双向扩展文件的信息。 端口监视器在端口初始化过程中使用此信息。

下面的示例显示了 `BidiFiles` INI 文件的部分。 该 `BidiSPMFile` 条目将用于标准 tcp/ip 端口监视器，该 `BidiWSDFile` 条目将用于 (WSD) 端口监视器的设备的 Web 服务。

```INI
# OEM Mapping & Extension GDL files 
# 
[BidiFiles]
BidiSPMFile = BidiSPM_AcmeXXX.XML
BidiWSDFile  = BidiWSD_AcmeXXX.XML
```
