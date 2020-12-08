---
title: SymStore 命令行选项
description: SymStore 事务支持以下语法形式。 第一个参数必须始终是 add 或 del。其他参数的顺序为重要。
keywords:
- SymStore Command-Line 选项 Windows 调试
ms.date: 03/12/2019
topic_type:
- apiref
api_name:
- SymStore Command-Line Options
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 50ef343708b3e53a88374e813e96c0b41bc7d3ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826929"
---
# <a name="symstore-command-line-options"></a>SymStore 命令行选项

SymStore 事务支持以下语法形式。 第一个参数是 **add**、 **query** 或 **del**。使用 **/？** 显示可用选项。 

```dbgcmd
symstore add [/r] [/p [/l] [-:MSG Message] [-:REL] [-:NOREFS]] /f File /s Store /t Product [/v Version] [/o] [/c Comment] [/d LogFile] [/compress]

symstore add [/r] [/p [/l] [-:REL] [-:NOREFS]] /g Share /f File /x IndexFile [/a] [/o] [/d LogFile] 

symstore add /y IndexFile /g Share /s Store [/p [-:MSG Message] [-:REL] [-:NOREFS]] /t Product [/v Version] [/o] [/c Comment] [/d LogFile] [/compress]

symstore query [/r] /f File /s Store [/o] [/d LogFile]

symstore del /i ID /s Store [/o] [/d LogFile] 

symstore /? 
```

## <a name="span-idddk_symstore_command_line_options_dbgspanspan-idddk_symstore_command_line_options_dbgspanparameters"></a><span id="ddk_symstore_command_line_options_dbg"></span><span id="DDK_SYMSTORE_COMMAND_LINE_OPTIONS_DBG"></span>参数


<span id="________f_______File______"></span><span id="________f_______file______"></span><span id="________F_______FILE______"></span>**/F** *文件*   
指定要添加的文件或目录的网络路径。

<span id="________g_______Share______"></span><span id="________g_______share______"></span><span id="________G_______SHARE______"></span>**/G** *共享*   
指定最初存储符号文件的服务器和共享。 与 **/f** 一起使用时， *Share* 应与 *文件* 说明符的开头相同。 与 **/y** 一起使用时， *Share* 应该是原始符号文件的位置，而不是索引文件)  (。 这允许您在以后更改文件路径的此部分，以防您将符号文件移动到其他服务器并共享。

<span id="________s_______Store______"></span><span id="________s_______store______"></span><span id="________S_______STORE______"></span>**/S** *存储*   
指定符号存储区的根目录。

<span id="________m_______Prefix______"></span><span id="________m_______prefix______"></span><span id="________M_______PREFIX______"></span>**/M** *前缀*   
使 SymStore 在存储文件或更新指针时更倾向于使用以 *前缀* 开头的路径中的符号。 此选项不能与 **/x** 选项一起使用。

<span id="________h___PUB___PRI__"></span><span id="________h___pub___pri__"></span><span id="________H___PUB___PRI__"></span>**/h** { **PUB |PRI** }  
如果在存储或更新符号时) 指定了 PRI，则会导致 SymStore 使用公共符号 (如果指定了 PUB) 或私有符号 (如果已指定 PRI。 此选项对二进制文件不起作用。

<span id="________i_______ID______"></span><span id="________i_______id______"></span><span id="________I_______ID______"></span>**/I** *ID*   
指定事务 ID 字符串。

<span id="________p______"></span><span id="________P______"></span>**/p**   
导致 SymStore 存储指向文件的指针，而不是文件本身。

<span id="________l______"></span><span id="________L______"></span>**/l**   
允许 *文件* 指定的文件位于本地目录中，而不是网络路径中。  (仅当使用 **/f** 和 **/p** 时才能使用此选项。 ) 

<span id="_______-_MSG________Message______"></span><span id="_______-_msg________message______"></span><span id="_______-_MSG________MESSAGE______"></span>**-： MSG** *消息*   
将指定的 *消息* 添加到每个文件中。  (仅当使用 **/p** 时才能使用此选项。 ) 

<span id="_______-_REL______"></span><span id="_______-_rel______"></span>**-： REL**   
允许文件指针中的路径是相对路径。 此选项表示/**l** 选项。  (仅当使用 **/p** 时才能使用此选项。 ) 

<span id="_______-_NOREFS______"></span><span id="_______-_norefs______"></span>**-： NOREFS**   
省略为正在存储的文件和指针创建引用指针文件。 仅当使用此选项创建了要更改的存储时，此选项才会在首次创建符号存储区时有效。

<span id="________r______"></span><span id="________R______"></span>**/r**   
使 SymStore 以递归方式添加文件或目录。

<span id="________t_______Product______"></span><span id="________t_______product______"></span><span id="________T_______PRODUCT______"></span>**/T** *产品*   
指定产品的名称。

<span id="________v_______Version______"></span><span id="________v_______version______"></span><span id="________V_______VERSION______"></span>**/V** *版本*   
指定产品的版本。

<span id="________c_______Comment______"></span><span id="________c_______comment______"></span><span id="________C_______COMMENT______"></span>**/c** *注释*   
指定事务的注释。

<span id="________d_______LogFile______"></span><span id="________d_______logfile______"></span><span id="________D_______LOGFILE______"></span>**/D** *日志文件*   
指定要用于命令输出的日志文件。 如果未包含此内容，则会将事务信息和其他输出发送到 **stdout**。

<span id="________o______"></span><span id="________O______"></span>**/o**   
导致 SymStore 显示详细输出。

<span id="________x_______IndexFile______"></span><span id="________x_______indexfile______"></span><span id="________X_______INDEXFILE______"></span>**/X** *IndexFile*   
导致 SymStore 不存储实际的符号文件。 相反，SymStore 记录 *IndexFile* 中的信息，这些信息将允许 SymStore 在以后访问符号文件。

<span id="________a______"></span><span id="________A______"></span>**/a**   
导致 SymStore 将新的索引信息追加到现有的索引文件。  (此选项仅与 **/x** 选项一起使用。 ) 

<span id="________y_______IndexFile______"></span><span id="________y_______indexfile______"></span><span id="________Y_______INDEXFILE______"></span>**/Y** *IndexFile*   
使 SymStore 从使用 **/x** 创建的文件中读取数据。

<span id="________yi_______IndexFile______"></span><span id="________yi_______indexfile______"></span><span id="________YI_______INDEXFILE______"></span>**/Yi** *IndexFile*   
向使用/**x** 选项创建的索引文件的末尾追加一个带有事务 ID 的注释。

<span id="________z___PUB___PRI__"></span><span id="________z___pub___pri__"></span><span id="________Z___PUB___PRI__"></span>**/z** { **PUB |PRI** }  
使 SymStore 仅对指定的符号类型进行索引。 如果指定了 **PUB** ，则只会为已去除完整源信息的符号编制索引。 如果指定了 **PRI** ，则只会为包含完整源信息的符号编制索引。 SymStore 将始终为二进制符号编制索引。

<span id="________compress______"></span><span id="________COMPRESS______"></span>**/compress**   
导致 SymStore 创建复制到符号存储区的每个文件的压缩版本，而不是使用该文件的未压缩副本。 仅当存储文件而不是指针时，此选项才有效，因此，在使用 **/p** 选项时不能使用此选项。

<span id="_______________"></span> **/?**   
显示 SymStore 命令的帮助文本。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 SymStore 的详细信息，请参阅 [使用符号服务器和符号存储](symbol-stores-and-symbol-servers.md)。









