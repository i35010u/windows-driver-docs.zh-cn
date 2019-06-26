---
title: 打印机 INF 文件的 Install 节
description: 打印机 INF 文件的 Install 节
ms.assetid: fb544271-1f0f-4bbd-b0a7-88dc89cc8186
keywords:
- INF 文件 WDK 打印，请安装部分
- 安装部分 WDK 打印机
- 部分 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41dab3bc7450df891d7b6e712895e74d3921241b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356038"
---
# <a name="printer-inf-file-install-sections"></a>打印机 INF 文件的 Install 节





Windows NT 4.0 和上一个供应商提供给客户的微型驱动程序还提供一份相应 Microsoft 打印机驱动程序，从 Microsoft 获取的客户。

通常，Windows 2000 和更高版本，供应商不能分发其微型驱动程序以及 Microsoft 的打印机驱动程序。 相反，每个供应商提供了安装供应商的文件，并调用 Microsoft 的打印机 INF 文件，Ntprint.inf，安装适当的打印机驱动程序组件的 INF 文件。

**请注意**   Microsoft 定期发布的打印机驱动程序的更新的版本。需要仅在更新版本中可用的功能的微型驱动程序可能需要额外的步骤。 有关详细信息，请参阅[使用更新的核心打印驱动程序](using-updated-core-print-drivers.md)。

 

Microsoft 的打印机 INF 文件，Ntprint.inf，包含以下[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)供应商 INF 文件，可以引用的：

-   \[PSCRIPT.OEM\]

    安装 Microsoft Postscript 打印机驱动程序 (Pscript)。

-   \[UNIDRV.OEM\]

    安装 Microsoft 通用打印机驱动程序 (Unidrv)。

-   \[UNIDRV\_BIDI.OEM\]

    安装 Microsoft 通用打印机驱动程序和 Pjlmon.dll，*语言监视器*的支持打印机作业语言 (PJL)，并提供 PJL 打印机的双向通信。

-   \[TTFSUB.OEM\]

    安装 Ttfsub.gpd，其中包含使用 Windows Driver Kit (WDK) 中，包含一组\*TTFS 常见 TrueType 字体替换功能，可用于支持 Unidrv 的打印机的条目。

-   \[sRGBPROFILE.OEM\]

    安装系统的 sRGB 颜色配置文件。

-   \[区域设置。OEM\]

    安装 Locale.gpd，其中包含区域设置标识符。 (请参阅[引用的区域设置](referencing-locales.md)。)

若要从您的 INF 文件中引用这些安装部分，该文件必须使用 Include，并且需要指令，如下面的示例中所示：

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

 

 




