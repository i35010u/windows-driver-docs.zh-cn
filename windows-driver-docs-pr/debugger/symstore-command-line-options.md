---
title: SymStore 命令行选项
description: 以下语法窗体的 SymStore 事务支持。 第一个参数必须始终将添加或 del。其他参数的顺序并不重要。
ms.assetid: 44009878-8f8a-4301-b075-eb0164b4f3a3
keywords:
- SymStore 命令行选项 Windows 调试
ms.date: 03/12/2019
topic_type:
- apiref
api_name:
- SymStore Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eb14a734528f9798126eecabe898fe63a3617240
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368023"
---
# <a name="symstore-command-line-options"></a>SymStore 命令行选项

以下语法窗体的 SymStore 事务支持。 第一个参数是**添加**，**查询**或**del**。使用 **/？** 若要显示可用的选项。 

```dbgcmd
symstore add [/r] [/p [/l] [-:MSG Message] [-:REL] [-:NOREFS]] /f File /s Store /t Product [/v Version] [/o] [/c Comment] [/d LogFile] [/compress]

symstore add [/r] [/p [/l] [-:REL] [-:NOREFS]] /g Share /f File /x IndexFile [/a] [/o] [/d LogFile] 

symstore add /y IndexFile /g Share /s Store [/p [-:MSG Message] [-:REL] [-:NOREFS]] /t Product [/v Version] [/o] [/c Comment] [/d LogFile] [/compress]

symstore query [/r] /f File /s Store [/o] [/d LogFile]

symstore del /i ID /s Store [/o] [/d LogFile] 

symstore /? 
```

## <a name="span-idddksymstorecommandlineoptionsdbgspanspan-idddksymstorecommandlineoptionsdbgspanparameters"></a><span id="ddk_symstore_command_line_options_dbg"></span><span id="DDK_SYMSTORE_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="________f_______File______"></span><span id="________f_______file______"></span><span id="________F_______FILE______"></span> **/f** *文件*   
指定文件或要添加的目录的网络的路径。

<span id="________g_______Share______"></span><span id="________g_______share______"></span><span id="________G_______SHARE______"></span> **/g** *Share*   
指定的服务器和共享了最初存储的符号文件。 与一起使用时 **/f**，*共享*应为相同的开头*文件*说明符。 与一起使用时 **/y**，*共享*应该是原始的符号文件 （而不是索引文件） 的位置。 这使您更高版本的更改的文件路径的这一部分将符号文件移到不同的服务器和共享的情况下。

<span id="________s_______Store______"></span><span id="________s_______store______"></span><span id="________S_______STORE______"></span> **/s** *应用商店*   
指定符号存储区的根目录。

<span id="________m_______Prefix______"></span><span id="________m_______prefix______"></span><span id="________M_______PREFIX______"></span> **/m** *Prefix*   
会导致以更倾向于使用开头的路径中的符号的 SymStore*前缀*存储文件时或更新的指针。 此选项不能用于 **/x**选项。

<span id="________h___PUB___PRI__"></span><span id="________h___pub___pri__"></span><span id="________H___PUB___PRI__"></span> **/h** { **PUB |PRI** }  
导致 SymStore 来更倾向于使用公共符号 （如果指定了发布） 或私有符号 （如果指定了 PRI） 存储或更新的符号时。 此选项具有二进制文件没有影响。

<span id="________i_______ID______"></span><span id="________i_______id______"></span><span id="________I_______ID______"></span> **/i** *ID*   
指定的事务 ID 字符串。

<span id="________p______"></span><span id="________P______"></span> **/p**   
导致 SymStore 存储指向该文件，而不是文件本身。

<span id="________l______"></span><span id="________L______"></span> **/l**   
允许指定的文件*文件*位于本地目录而不是网络路径。 (只能是此选项时使用这两 **/f**和 **/p**使用。)

<span id="_______-_MSG________Message______"></span><span id="_______-_msg________message______"></span><span id="_______-_MSG________MESSAGE______"></span> **-:MSG** *Message*   
添加指定*消息*到每个文件。 (此选项仅可使用何时 **/p**使用。)

<span id="_______-_REL______"></span><span id="_______-_rel______"></span> **-:REL**   
允许在文件指针是相对路径。 此选项意味着 /**l**选项。 (此选项仅可使用何时 **/p**使用。)

<span id="_______-_NOREFS______"></span><span id="_______-_norefs______"></span> **-:NOREFS**   
忽略的文件和存储的指针的引用指针文件创建。 此选项才有效在符号存储区的初始创建期间如果要更改的存储区创建使用此选项。

<span id="________r______"></span><span id="________R______"></span> **/r**   
若要添加文件或目录以递归方式的原因 SymStore。

<span id="________t_______Product______"></span><span id="________t_______product______"></span><span id="________T_______PRODUCT______"></span> **/t** *产品*   
指定的产品名称。

<span id="________v_______Version______"></span><span id="________v_______version______"></span><span id="________V_______VERSION______"></span> **/v** *版本*   
指定的产品版本。

<span id="________c_______Comment______"></span><span id="________c_______comment______"></span><span id="________C_______COMMENT______"></span> **/c** *注释*   
指定事务的注释。

<span id="________d_______LogFile______"></span><span id="________d_______logfile______"></span><span id="________D_______LOGFILE______"></span> **/d** *LogFile*   
指定要用于命令输出的日志文件。 如果这不包括，事务信息和其他输出发送到**stdout**。

<span id="________o______"></span><span id="________O______"></span> **/o**   
导致 SymStore 以显示详细输出。

<span id="________x_______IndexFile______"></span><span id="________x_______indexfile______"></span><span id="________X_______INDEXFILE______"></span> **/x** *IndexFile*   
导致 SymStore 不用于存储实际的符号文件。 相反，SymStore 记录中的信息*索引文件，所以*，使 SymStore 在更高版本时访问的符号文件。

<span id="________a______"></span><span id="________A______"></span> **/a**   
若要将新的索引信息添加到现有索引文件的原因 SymStore。 (此选项仅用于 **/x**选项。)

<span id="________y_______IndexFile______"></span><span id="________y_______indexfile______"></span><span id="________Y_______INDEXFILE______"></span> **/y** *IndexFile*   
导致要从使用创建的文件中读取数据的 SymStore **/x**。

<span id="________yi_______IndexFile______"></span><span id="________yi_______indexfile______"></span><span id="________YI_______INDEXFILE______"></span> **/yi** *IndexFile*   
使用创建的索引文件的末尾追加事务 id 的注释 /**x**选项。

<span id="________z___PUB___PRI__"></span><span id="________z___pub___pri__"></span><span id="________Z___PUB___PRI__"></span> **/z** { **PUB | PRI** }  
导致 SymStore 索引仅指定的符号的类型。 如果**PUB**指定，将索引已去除的完整源代码信息符号。 如果**PRI**指定，将索引只能包含完整的源信息的符号。 SymStore 始终将索引二进制符号。

<span id="________compress______"></span><span id="________COMPRESS______"></span> **/compress**   
导致 SymStore 若要创建的每个文件复制到符号存储区而不是使用未压缩的文件的副本的压缩的版本。 当存储文件和而不是指针时，此选项才有效，因此无法使用时 **/p**使用选项。

<span id="_______________"></span> **/?**   
显示帮助 SymStore 命令的文本。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 SymStore 详细信息，请参阅[使用符号服务器和符号存储区](symbol-stores-and-symbol-servers.md)。









