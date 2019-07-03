---
title: 使用帮助文档
description: 使用帮助文档
ms.assetid: ad826f45-3bad-4e10-811f-26ebf4f06c4d
keywords:
- HTML 帮助
- 搜索帮助文件
- 帮助文件的索引
- 帮助文件中的收藏夹
- 帮助文件中的打印主题
- hh.exe
- 帮助文件
- 帮助文件，概述
- 帮助文件，搜索
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f4da4720ead1e1c9f04a32cae1e02968525286e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340493"
---
# <a name="using-the-help-documentation"></a>使用帮助文档


## <span id="ddk_using_the_help_file_dbg"></span><span id="DDK_USING_THE_HELP_FILE_DBG"></span>


你正在阅读的 WinDbg 帮助文档是有关 Windows 调试工具软件包的文档。

本文档使用 Microsoft HTML 帮助 (hh.exe) 提供的查看器。 此查看器提供的目录和索引的表和可让你搜索通过文档时，将你最喜爱的或经常使用主题和打印的一个或多个主题。

本主题中的下列部分描述的功能以及如何使用帮助文档。

### <a name="span-idcontentstabspanspan-idcontentstabspancontents-tab"></a><span id="contents_tab"></span><span id="CONTENTS_TAB"></span>内容选项卡

**内容**选项卡提供了内容的文档的表的可展开视图。

单击加号 ( **+** ) 的节点旁边或双击要展开或折叠该节点下的目录中的节点的标题。

### <a name="span-idindextabspanspan-idindextabspanindex-tab"></a><span id="index_tab"></span><span id="INDEX_TAB"></span>索引选项卡

**索引**选项卡显示在本文档中使用的术语的完整索引。 可以输入一个词的开头，也可以使用滚动条来浏览此索引。

### <a name="span-idsearchtabspanspan-idsearchtabspansearch-tab"></a><span id="search_tab"></span><span id="SEARCH_TAB"></span>搜索选项卡

在中**搜索**任何单词或短语的文档中包含的选项卡上，可以搜索。 可以搜索所有文本，也可以限制对主题标题进行都搜索。

若要搜索包含多个单词的短语，请将该短语用引号引起来。 您可以连接多个单词和短语与 AND、 OR 和 NOT 运算符。 默认运算符是 and。

请注意，"AND NOT"无效。 若要搜索包含的话题*x*而不*y*，使用"*x*不*y*"。 此外可以使用 NEAR 搜索中。

此外允许使用通配符。 使用问号 ( **？** ) 来表示任何单个字符和一个星号 (* *\\* * *) 来表示零个或多个字符。 但是，不能使用带引号的字符串中的通配符。

所有字母和数字将被都视为按字面意思，但在搜索中不允许使用某些符号。

搜索返回与指定的条件匹配的所有主题的列表。 如果选择**搜索以前的结果**框中，然后搜索更多条款这些结果。

### <a name="span-idfavoritestabspanspan-idfavoritestabspanfavorites-tab"></a><span id="favorites_tab"></span><span id="FAVORITES_TAB"></span>收藏夹选项卡

在中**收藏夹**选项卡上，您可以保存经常访问的主题的标题。 在你查看主题，请单击**收藏夹**选项卡，然后单击**添加**按钮。

若要重命名您的收藏夹列表上的页面，速度慢，两次单击其名称并重新键入名称。 若要查看的收藏夹列表上的主题，请双击其名称或一次单击，然后单击**显示**。 若要从收藏夹列表中删除一个主题，请单击它一次，然后单击**删除**。

### <a name="span-idprintingtopicsspanspan-idprintingtopicsspanprinting-topics"></a><span id="printing_topics"></span><span id="PRINTING_TOPICS"></span>打印主题

若要打印一个或多个主题，请单击中的主题**内容**选项卡，然后依次**打印**工具栏上的按钮。 系统将询问是否想要打印仅所选的主题或该主题及其所有及其子主题。

此外可以打印正在查看内视图窗口中，右键单击，单击主题**打印**快捷菜单上。 但是，此方法不能让您打印子主题。

### <a name="span-idsearchingwithinatopicspanspan-idsearchingwithinatopicspansearching-within-a-topic"></a><span id="searching_within_a_topic"></span><span id="SEARCHING_WITHIN_A_TOPIC"></span>在本主题中搜索

若要搜索你正在查看的主题内的文本字符串，请按 CTRL + F，或单击**本主题中查找**上**编辑**菜单。

### <a name="span-idaccessingthehelpdocumentationspanspan-idaccessingthehelpdocumentationspanaccessing-the-help-documentation"></a><span id="accessing_the_help_documentation"></span><span id="ACCESSING_THE_HELP_DOCUMENTATION"></span>访问帮助文档

若要打开此帮助文档，请执行以下操作：

-   单击**启动**，依次指向**所有程序**，指向**有关 Windows 调试工具**，然后单击**调试帮助**。

-   打开 Windows 资源管理器中，找到 Debugger.chm 文件，然后双击它。

-   在命令提示符处，浏览到包含 Debugger.chm 和运行的文件夹**hh debugger.chm**。

-   在任何 Windows 调试器中，使用[ **.hh （打开 HTML 帮助文件）** ](-hh--open-html-help-file-.md)命令。

-   在 WinDbg 中，单击**内容**上**帮助**菜单。 此命令打开帮助文档，并打开**内容**选项卡。

-   在 WinDbg 中，单击**索引**上**帮助**菜单。 此命令打开帮助文档，并打开**索引**选项卡。

-   在 WinDbg 中，单击**搜索**上**帮助**菜单。 此命令将打开帮助文档，并打开**搜索**选项卡。

-   在 WinDbg 中的许多对话框都**帮助**按钮。 单击**帮助**以打开此文档，并打开相关的页面。

 

 





