---
title: 打印机 INF 文件的 Data 节
description: 打印机 INF 文件的 Data 节
keywords:
- INF 文件 WDK 打印，数据部分
- 数据部分 WDK 打印机
- 以前的名称数据部分 WDK 打印机
- 部分 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f7d4ddadbaf2c7722aa4a3f11866fe876979ab1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807273"
---
# <a name="printer-inf-file-data-sections"></a>打印机 INF 文件的 Data 节





默认的 Windows 2000 和更高版本的打印机类安装程序 Ntprint.dll，它允许打印机 INF 文件包含数据部分。 使用以下格式指定数据节：

**DataSection** = *SectionName*

其中 *SectionName* 是一个 INF 文件部分名称。

数据节用于指定多个打印机共用的 [打印机 INF 文件条目](printer-inf-file-entries.md) 集。 通过在命名部分下对列表中的常见条目进行分组，然后在使用条目的每个打印机的 **DataSection** 语句中引用该部分，该条目列表仅在 INF 文件中包含一次。

Microsoft 的打印机 INF 文件 Ntprint.inf 定义以下数据部分：

-   \[PSCRIPT \_ 数据\]

    为 Microsoft PostScript 打印机驱动程序 **ConfigFile** 的 DriverFile、 **DriverFile** 和 **帮助** 项分配值。

-   \[UNIDRV \_ 数据\]

    为 Microsoft 通用打印机驱动程序 **ConfigFile** 的 DriverFile、 **DriverFile** 和 **帮助** 项分配值。

-   \[UNIDRV \_ 双向 \_ 数据\]

    为双向打印机的 Microsoft 通用 **ConfigFile** 打印机驱动 **HelpFile** 程序将值 **LanguageMonitor** 分配给 **DriverFile**、

应从供应商提供的 INF 文件中引用这些数据部分。 有关示例，请参阅 [安装 Unidrv 微型驱动程序](installing-a-unidrv-minidriver.md) 和 [安装 Pscript 微型驱动程序](installing-a-pscript-minidriver.md)。

**注意**   具有 " **需要** " 条目的 IHV 打印机 INF 文件或引用 Ntprint.inf 的 **Include** 条目不能包含与 ntprint.inf 中存在的任何 INF 节名称相同的数据节名称。 在为供应商提供的打印机 INF 文件中的数据分区命名之前，请搜索% windir%/inf/Ntprint.inf，以确保你的节名在 Ntprint.inf 内的任何类型)  (。

 

### <a name="previous-names-section"></a><a href="" id="ddk--previous-names-section-gg"></a>"先前名称" 部分

Windows 2000 和更高版本的打印机类安装程序可识别称为 "以前的名称" 的特殊数据部分。 每个 INF 文件中允许使用其中一种部分。 部分中的条目标识与 Windows 2000 和更高版本的打印机名称不同于 Windows 95/98/Me 的驱动程序。 指定此类名称差异后，连接到 Windows 2000 和更高版本服务器的 Windows 95/98/Me 客户端就可以支持定点和打印。

本节中每个条目的格式为：

"*Windows 2000 或更高版本的打印机名称*" = "*windows 95/98/Me printer name*"

下面是示例条目：

```cpp
[Previous Names]
"HP Color LaserJet" = "HP Color LaserJet (MS)"
"HP DeskJet 1200C" = "HP DeskJet 1200C (MS)"
"HP DeskJet 310" = "HP DeskJet 310 Printer"
```

 

 




