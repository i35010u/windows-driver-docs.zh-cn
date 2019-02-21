---
title: AgeStore 命令行选项
description: AgeStore 命令行使用以下语法。 可以按任意顺序包含参数。
ms.assetid: ae6ad504-a582-45ac-89a1-7e90952948b4
keywords:
- AgeStore 命令行选项 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AgeStore Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 00e28de127720c66f1c0fbd32ce3822069818eb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523357"
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

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______PathSpec______"></span><span id="_______pathspec______"></span><span id="_______PATHSPEC______"></span> *PathSpec*   
指定是用要删除的文件的目标目录。 如果使用-s 选项，则*PathSpec*指定目标树是用要删除的文件的根目录。 *PathSpec*可能是本地计算机上的目录的绝对或相对路径或 UNC 路径。 如果*PathSpec*包含空格，则必须用引号引起来。 如果*PathSpec*是省略，AgeStore 使用当前工作目录。

<span id="-date_Month-Day-Year"></span><span id="-date_month-day-year"></span><span id="-DATE_MONTH-DAY-YEAR"></span>**-date=**<em>Month-Day-Year</em>  
指定用于删除文件的截止日期。 上次访问指定日期之前的所有文件将被都删除。 必须以连字符结尾之间日和年和月和日之间的月-日-年格式指定的日期。 的前导零*月*并*天*都是可选的。 可以使用两位数或四个指定年份。 因此，您可以指示 2008 年 1 月 5 日的日期为 01-05-2008 或 1-5-08。

<span id="_______-days_NumberOfDays______"></span><span id="_______-days_numberofdays______"></span><span id="_______-DAYS_NUMBEROFDAYS______"></span> **-days=**<em>NumberOfDays</em>   
指定截止日期和时间删除文件。 上次访问指定的天前数之前的所有文件将被都删除。 *NumberOfDays*指定整数值 24 小时制。 例如，如果说明符-天 = 3 使用在 2008 年 2 月 17 日下午 6:00，在 2008 年 2 月 14 日下午 6:00 之前最后一次访问的所有文件将被都删除。

<span id="_______-size_SizeRemaining______"></span><span id="_______-size_sizeremaining______"></span><span id="_______-SIZE_SIZEREMAINING______"></span> **-size=**<em>SizeRemaining</em>   
指定应保留后删除，以字节为单位的文件的总大小。 如果使用此开关，AgeStore 删除目标目录或目标树中的文件、 文件开头最近访问过最少，直到剩余文件的总大小小于或等于*SizeRemaining*。 当 **-s**选项，则 AgeStore 面向整个目录树，并*SizeRemaining*后删除此整个目录树中指定应保留的文件的总大小。

<span id="_______-size______"></span><span id="_______-SIZE______"></span> **-size**   
若要列出的目标目录或目标树中的所有文件的总大小的原因 AgeStore。 不删除任何文件。

<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *选项*   
以下选项的任意组合。

<span id="-l"></span><span id="-L"></span>**-l**  
AgeStore 不要删除任何文件，而只是为了要列出这一相同命令已运行而不会删除的所有文件将导致 **-l**选项。

<span id="-s"></span><span id="-S"></span>**-s**  
会导致将属于的整个目录树的 AgeStore *PathSpec*作为目标。 当 **-s**不使用选项，指定的目录*PathSpec*变得不会在其中删除文件的目标目录。 当 **-s**使用选项，则指定的目录*PathSpec*和其下的所有子目录都成为目标树中删除文件。

<span id="-k"></span><span id="-K"></span>**-k**  
导致 AgeStore 保留为空的任何子目录。 如果不使用此选项，AgeStore 将删除目标目录，如果命令运行后，它是完全为空。 如果 **-s**而不使用选项 **-k**选项，目标目录树中的所有空目录后，将删除 AgeStore 已完成文件删除-甚至根目录本身，如果它将成为为空。 如果发生这种情况为已空 AgeStore 运行之前在此树中的目录，AgeStore 删除以及这些目录。 但是，如果 AgeStore 命令不导致删除任何文件 (例如，如果 **-大小 =**<em>SizeRemaining</em>参数在目标树中指定的大小大于所有文件的总大小)、 为空不会删除目录。 如果 **-s**不使用选项时，永远不会删除空的目录，并 **-k**选项将被忽略。

<span id="-q"></span><span id="-Q"></span>**-q**  
安静模式。 如果未包括此选项，则 AgeStore 将列出所有文件，因为删除它们。

<span id="-y"></span><span id="-Y"></span>**-y**  
禁止显示 **（是/否）** 提示符。 如果不使用此选项，AgeStore 会提示你使用"确实吗？" 删除任何文件之前进行提示。

<span id="_______-_______"></span> **-?**   
显示帮助文本 AgeStore 命令行。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 AgeStore 工具的详细信息，请参阅[使用 AgeStore](using-agestore.md)。

 

 





