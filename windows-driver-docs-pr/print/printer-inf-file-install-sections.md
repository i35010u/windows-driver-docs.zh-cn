---
title: 打印机 INF 文件的 Install 节
description: 打印机 INF 文件的 Install 节
keywords:
- INF 文件 WDK 打印，安装部分
- 安装部分 WDK 打印机
- 部分 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4d6e80c6b27a6f95bc37540dac4bdd54da5c57b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807263"
---
# <a name="printer-inf-file-install-sections"></a>打印机 INF 文件的 Install 节





对于 Windows NT 4.0 及更早版本，向客户提供微型驱动程序的供应商还向客户提供了从 Microsoft 获得的相应 Microsoft 打印机驱动程序的副本。

通常，对于 Windows 2000 及更高版本，供应商不会将 Microsoft 的打印机驱动程序与微型驱动程序一起分发。 相反，每个供应商提供一个 INF 文件来安装供应商的文件，然后调用 Microsoft 的打印机 INF 文件 Ntprint.inf，该文件又会安装相应的打印机驱动程序组件。

**注意**   Microsoft 会定期发布其打印机驱动程序的更新版本。只需要在更新版本中使用的功能的微型驱动程序可能需要额外的步骤。 有关详细信息，请参阅 [使用更新的核心打印驱动程序](using-updated-core-print-drivers.md)。

 

Microsoft 的打印机 INF 文件（Ntprint.inf）包含以下 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md) ，可供供应商 INF 文件引用：

-   \[PSCRIPT.原始\]

     (Pscript) 安装 Microsoft Postscript 打印机驱动程序。

-   \[UNIDRV.原始\]

     (Unidrv) 安装 Microsoft 通用打印机驱动程序。

-   \[UNIDRV \_ 双向。原始\]

    安装 Microsoft 通用打印机驱动程序和 Pjlmon.dll，支持打印机作业语言的 *语言监视器* (PJL) ，并为 PJL 打印机提供双向通信。

-   \[TTFSUB.原始\]

    安装 Ttfsub gpd，它随 Windows 驱动程序工具包 (WDK) 提供，并包含一组 \* 用于常见 TrueType 字体替换的 TTFS 条目，可用于 Unidrv 支持的打印机。

-   \[sRGBPROFILE\]

    安装系统的 sRGB 颜色配置文件。

-   \[本地.原始\]

    安装 gpd，其中包含区域设置标识符。  (参阅 [引用区域设置](referencing-locales.md)。 ) 

若要从 INF 文件中引用这些安装部分，文件必须使用 Include 和需求指令，如以下示例中所示：

```cpp
[Manufacturer]
"ABC Printers"
 
[ABC Printers]
"ABC Printer 100ex" = ABC100EX.GPD, ABC_Printer_100ex
 
[ABC100EX.GPD]
CopyFiles=@ABCres.dll,@ABC100EX.gpd
DataSection=UNIDRV_BIDI_DATA      ; Unidrv Bidirectional Data Section
DataFile=ABC100EX.gpd
Include=NTPRINT.INF               ; Include NTPRINT.INF.
Needs=TTFSUB.OEM,UNIDRV_BIDI.OEM  ; Install Unidrv, TrueType subs,
 ;    and PJL language monitor.
```

 

