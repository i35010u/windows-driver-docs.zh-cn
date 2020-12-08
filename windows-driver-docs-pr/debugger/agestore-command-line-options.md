---
title: AgeStore 命令行选项
description: AgeStore 命令行使用以下语法。 可以按任意顺序包含参数。
keywords:
- AgeStore Command-Line 选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AgeStore Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1b937dafa26fe560453e2c623f0a3d2f048e7207
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808517"
---
# <a name="agestore-command-line-options"></a>AgeStore 命令行选项


AgeStore 命令行使用以下语法。 可以按任意顺序包含参数。

```console
agestore [PathSpec] -date=Month-Day-Year Options 

agestore [PathSpec] -days=NumberOfDays Options 

agestore [PathSpec] -size=SizeRemaining Options 

agestore [PathSpec] -size Options 

agestore -? 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______PathSpec______"></span><span id="_______pathspec______"></span><span id="_______PATHSPEC______"></span>*PathSpec*   
指定要在其中删除文件的目标目录。 如果使用-s 选项，则 *PathSpec* 指定要在其中删除文件的目标树的根目录。 *PathSpec* 可以是本地计算机上某个目录的绝对路径或相对路径，也可以是 UNC 路径。 如果 *PathSpec* 包含空格，则必须用引号将其引起来。 如果省略 *PathSpec* ，则 AgeStore 将使用当前工作目录。

<span id="-date_Month-Day-Year"></span><span id="-date_month-day-year"></span><span id="-DATE_MONTH-DAY-YEAR"></span>**-日期 =**<em>月份</em>-每年  
指定删除文件的截止日期。 将删除上次在指定日期之前访问的所有文件。 日期必须以月/日的格式指定，并在月和日之间以及在 day 和 Year 之间。 *月份* 和 *日期* 中的前导零是可选的。 可以用两位数或四个数字来指定年份。 因此，可以指示2008年1月5日（1-5-08 01-05-2008）的日期。

<span id="_______-days_NumberOfDays______"></span><span id="_______-days_numberofdays______"></span><span id="_______-DAYS_NUMBEROFDAYS______"></span>**-days =**<em>NumberOfDays</em>   
指定删除文件的截止日期和时间。 在指定的天数前最后访问的所有文件将被删除。 *NumberOfDays* 指定24小时内的整数。 例如，如果在6:00 年2月 17 2008 日下午使用说明符-days = 3，则在2月 2008 14 日6:00 之前访问的所有文件都将被删除。

<span id="_______-size_SizeRemaining______"></span><span id="_______-size_sizeremaining______"></span><span id="_______-SIZE_SIZEREMAINING______"></span>**-size =**<em>SizeRemaining</em>   
指定在删除之后应该保留的文件的总大小（以字节为单位）。 使用此开关时，AgeStore 会删除目标目录或目标树中的文件（以最近访问的文件开头），直到剩余文件的总大小小于或等于 *SizeRemaining*。 使用 **-s** 选项时，AgeStore 将以整个目录树为目标， *SizeRemaining* 指定删除后应保留在此整个目录树中的文件的总大小。

<span id="_______-size______"></span><span id="_______-SIZE______"></span>**-size**   
使 AgeStore 列出目标目录或目标树中所有文件的总大小。 不删除任何文件。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
以下选项的任意组合。

<span id="-l"></span><span id="-L"></span>**-l**  
导致 AgeStore 不删除任何文件，只是列出在运行此同一命令但不包含 **-l** 选项的所有文件。

<span id="-s"></span><span id="-S"></span>**-s**  
使 AgeStore *将作为目标* 的整个目录树作为目标处理。 如果未使用 **-s** 选项，则 *PathSpec* 指定的目录将成为要在其中删除文件的目标目录。 使用 **-s** 选项时， *PathSpec* 指定的目录及其下的所有子目录将成为要在其中删除文件的目标树。

<span id="-k"></span><span id="-K"></span>**-k**  
使 AgeStore 保留任何空的子目录。 如果未使用此选项，则在命令运行后，AgeStore 将删除目标目录（如果它完全为空）。 如果在不使用 **-k** 选项的情况下使用 **-s** 选项，则在 AgeStore 完成文件删除后，将删除目标目录树中的所有空目录（即使根目录本身为空）。 如果此树中有一些在 AgeStore 运行之前已经为空的目录，则 AgeStore 也会删除这些目录。 但是，如果 AgeStore 命令导致不删除文件 (例如，如果 **-size =**<em>SizeRemaining</em> 参数指定的大小大于目标树中所有文件的总大小) ，则不会删除空目录。 如果未使用 **-s** 选项，则永远不会删除空目录，并忽略 **-k** 选项。

<span id="-q"></span><span id="-Q"></span>**-q**  
静默模式。 如果未包括此选项，则在删除所有文件时，AgeStore 将列出这些文件。

<span id="-y"></span><span id="-Y"></span>**-y**  
取消 **) 提示符 (** 。 如果未使用此选项，AgeStore 会提示你 "是否确实要这样做？" 删除任何文件前提示。

<span id="_______-_______"></span> **-?**   
显示 AgeStore 命令行的帮助文本。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 AgeStore 工具的详细信息，请参阅 [使用 AgeStore](using-agestore.md)。

 

 





