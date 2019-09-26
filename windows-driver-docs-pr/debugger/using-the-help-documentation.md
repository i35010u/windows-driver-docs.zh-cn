---
title: 使用帮助文档
description: 使用帮助文档
ms.assetid: ad826f45-3bad-4e10-811f-26ebf4f06c4d
keywords:
- HTML 帮助
- 搜索帮助文件
- 帮助文件的索引
- 帮助文件中的收藏夹
- 打印帮助文件中的主题
- cmd.exe
- 帮助文件
- 帮助文件，概述
- 帮助文件，搜索
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0969639f95a4c2033d02b517ebe96131c977c32
ms.sourcegitcommit: 9dbb1ef59c3e797bfc3cc418dd2b9bdc44940d14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71284884"
---
# <a name="using-the-help-documentation"></a>使用帮助文档


## <span id="ddk_using_the_help_file_dbg"></span><span id="DDK_USING_THE_HELP_FILE_DBG"></span>


您正在阅读的 WinDbg 帮助文档是适用于 Windows 包调试工具的文档。

本文档使用提供的查看器，该查看器与 Microsoft HTML 帮助（cmd.exe）一起提供。 此查看器提供了目录和索引，并使你能够搜索文档、标记你喜欢的主题或常用主题，以及打印一个或多个主题。

本主题中的以下部分介绍的功能以及如何使用帮助文档。

### <a name="span-idcontents_tabspanspan-idcontents_tabspancontents-tab"></a><span id="contents_tab"></span><span id="CONTENTS_TAB"></span>内容选项卡

"**内容**" 选项卡提供文档目录的可展开视图。

单击节点旁边的加号 **+** （）或双击该节点的标题，展开或收缩该节点下的目录。

### <a name="span-idindex_tabspanspan-idindex_tabspanindex-tab"></a><span id="index_tab"></span><span id="INDEX_TAB"></span>索引选项卡

"**索引**" 选项卡显示了本文档中使用的术语的完整索引。 您可以输入字词的开头或使用滚动条来浏览此索引。

### <a name="span-idsearch_tabspanspan-idsearch_tabspansearch-tab"></a><span id="search_tab"></span><span id="SEARCH_TAB"></span>搜索选项卡

在 "**搜索**" 选项卡中，可以搜索文档中包含的任何单词或短语。 您可以搜索所有文本或将搜索范围限制为主题标题。

若要搜索包含多个单词的短语，请将该短语用引号引起来。 可以通过 AND、OR 和 NOT 运算符来连接多个字词和短语。 默认运算符是和。

请注意，"AND NOT" 无效。 若要搜索包含*x*而不是*y*的主题，请使用 "*x* not *y*"。 你还可以在搜索中使用 NEAR。

还允许使用通配符。 使用问号（ **？** ）表示任何单个字符，使用星号（ **\*** ）表示零个或多个字符。 但是，不能在带引号的字符串中使用通配符。

所有字母和数字都按原义处理，但在搜索中不允许使用某些符号。

搜索将返回与指定条件匹配的所有主题的列表。 如果选择 "**搜索上一个结果**" 框，则可以在这些结果中搜索更多字词。

### <a name="span-idfavorites_tabspanspan-idfavorites_tabspanfavorites-tab"></a><span id="favorites_tab"></span><span id="FAVORITES_TAB"></span>收藏夹选项卡

在 "**收藏夹**" 选项卡中，你可以保存常用主题的标题。 在查看主题时，请单击 "**收藏夹**" 选项卡，然后单击 "**添加**" 按钮。

若要重命名收藏夹列表中的某个页面，请将其名称按慢两次，然后重新键入该名称。 若要查看 "收藏夹" 列表中的主题，请双击其名称或单击一次，然后单击 "**显示**"。 若要从 "收藏夹" 列表中删除某个主题，请单击一次，然后单击 "**删除**"。

### <a name="span-idprinting_topicsspanspan-idprinting_topicsspanprinting-topics"></a><span id="printing_topics"></span><span id="PRINTING_TOPICS"></span>打印主题

若要打印一个或多个主题，请在 "**内容**" 选项卡中单击某个主题，然后单击工具栏上的 "**打印**" 按钮。 系统将询问您是要仅打印选定的主题还是打印该主题及其所有子主题。

您还可以通过在 "视图" 窗口中右键单击，然后单击快捷菜单上的 "**打印**" 来打印您正在查看的主题。 但是，此方法不允许打印副标题。

### <a name="span-idsearching_within_a_topicspanspan-idsearching_within_a_topicspansearching-within-a-topic"></a><span id="searching_within_a_topic"></span><span id="SEARCHING_WITHIN_A_TOPIC"></span>在主题中搜索

若要在您正在查看的主题中搜索文本字符串，请按 CTRL + F，或在 "**编辑**" 菜单上单击**本主题中**的 "查找"。

### <a name="span-idaccessing_the_help_documentationspanspan-idaccessing_the_help_documentationspanaccessing-the-help-documentation"></a><span id="accessing_the_help_documentation"></span><span id="ACCESSING_THE_HELP_DOCUMENTATION"></span>访问帮助文档

若要打开此帮助文档，请执行以下操作之一：

-   单击 "**开始**"，指向 "**所有程序**"，指向 " **Windows 调试工具**"，然后单击 "**调试帮助**"。

-   打开 Windows 资源管理器，找到调试器 .chm 文件，然后双击该文件。

-   在命令提示符下，浏览到包含调试器的文件夹，然后运行**hh 调试器**。

-   在任何 Windows 调试器中，使用[ **.hh （打开 HTML 帮助文件）** ](-hh--open-html-help-file-.md)命令。

-   在 WinDbg 中，单击 "**帮助**" 菜单上的 "**内容**"。 此命令打开帮助文档并打开 "**内容**" 选项卡。

-   在 WinDbg 中，单击 "**帮助**" 菜单上的 "**索引**"。 此命令打开帮助文档并打开 "**索引**" 选项卡。

-   在 WinDbg 中，单击 "**帮助**" 菜单上的 "**搜索**"。 此命令打开帮助文档并打开 "**搜索**" 选项卡。

-   WinDbg 中的许多对话框都具有 "**帮助**" 按钮。 单击 "**帮助**" 以打开此文档并打开相关页面。

 

 





