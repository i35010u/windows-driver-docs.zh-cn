---
title: 创建自己的提供程序模块
description: 创建自己的提供程序模块
keywords:
- 版本控制系统，提供程序模块
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ab2261f6a57d3a4e905c2865d6f45c9af210d7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787821"
---
# <a name="creating-your-own-provider-module"></a>创建自己的提供程序模块


通常，若要创建自己的提供程序模块，必须实现以下接口集。

<span id="_module__SimpleUsage__"></span><span id="_module__simpleusage__"></span><span id="_MODULE__SIMPLEUSAGE__"></span>**$module：： SimpleUsage ( # B1**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
向 STDOUT 显示简单的模块使用情况信息。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**Parameters**  
无

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  
无

<span id="_module__VerboseUsage__"></span><span id="_module__verboseusage__"></span><span id="_MODULE__VERBOSEUSAGE__"></span>**$module：： VerboseUsage ( # B1**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
向 STDOUT 显示深入的模块使用情况信息。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**Parameters**  
无

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  
无

<span id="_objref____module__new__CommandArguments_"></span><span id="_objref____module__new__commandarguments_"></span><span id="_OBJREF____MODULE__NEW__COMMANDARGUMENTS_"></span>**$objref = $module：： new (** <em>@CommandArguments</em>**)**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
初始化提供程序模块的实例。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**Parameters**  

<span id="_CommandArguments"></span><span id="_commandarguments"></span><span id="_COMMANDARGUMENTS"></span><em>@CommandArguments</em>  
@ARGVSsindex.cmd 不能识别为常规参数的所有参数。

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  
可在后续操作中使用的引用。

<span id="_objref-_GatherFileInformation__SourcePath__ServerHashReference_"></span><span id="_objref-_gatherfileinformation__sourcepath__serverhashreference_"></span><span id="_OBJREF-_GATHERFILEINFORMATION__SOURCEPATH__SERVERHASHREFERENCE_"></span>**$objref- &gt;GatherFileInformation (** <em>$SourcePath</em>**，**<em>$ServerHashReference</em> **)**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
使模块能够为 *$SourcePath* 参数所指定的目录收集所需的源索引信息。 该模块不应假定每个对象只能调用一次此项 instancebecause Ssindex.cmd 可能会为不同的路径多次调用此项。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**Parameters**  

<span id="_SourcePath"></span><span id="_sourcepath"></span><span id="_SOURCEPATH"></span>*$SourcePath*  
包含要编制索引的源的本地目录。

<span id="_ServerHashReference"></span><span id="_serverhashreference"></span><span id="_SERVERHASHREFERENCE"></span>*$ServerHashReference*  
对包含指定 Srcsrv.ini 文件中所有条目的哈希值的引用。

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  
无

<span id="__VariableHashReference__FileEntry_____objref-_GetFileInfo__LocalFile_"></span><span id="__variablehashreference__fileentry_____objref-_getfileinfo__localfile_"></span><span id="__VARIABLEHASHREFERENCE__FILEENTRY_____OBJREF-_GETFILEINFO__LOCALFILE_"></span>**(** <em>$VariableHashReference</em>**，**<em>$FileEntry</em> **) = $objref** - &gt; **microsoft.visualbasic.fileio.filesystem.getfileinfo (** <em>$LocalFile</em> **)**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
提供必要的信息以从源代码管理系统中提取单个特定文件。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**Parameters**  

<span id="_LocalFile"></span><span id="_localfile"></span><span id="_LOCALFILE"></span>*$LocalFile*  
完全限定的文件名。

<span id="Return_Values"></span><span id="return_values"></span><span id="RETURN_VALUES"></span>**返回值**  

<span id="_VariableHashReference"></span><span id="_variablehashreference"></span><span id="_VARIABLEHASHREFERENCE"></span>*$VariableHashReference*  
解释返回的 *$FileEntry* 所需的变量的哈希引用。 Ssindex.cmd 将为单个调试文件使用的每个源文件缓存这些变量，以减少写入源索引流的信息量。

<span id="_FileEntry"></span><span id="_fileentry"></span><span id="_FILEENTRY"></span>*$FileEntry*  
要写入源索引流以允许 Srcsrv.ini 从源代码管理提取此文件的文件项。 此行的准确格式特定于源代码管理系统。

<span id="_TextString___objref-_LongName__"></span><span id="_textstring___objref-_longname__"></span><span id="_TEXTSTRING___OBJREF-_LONGNAME__"></span><em>$TextString</em>**= $Objref &gt; ( # B1**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
提供描述性字符串来向最终用户标识源代码管理系统。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**Parameters**  
无

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  

<span id="_TextString"></span><span id="_textstring"></span><span id="_TEXTSTRING"></span>*$TextString*  
源代码管理系统的描述性名称。

<span id="_StreamVariableLines__objref-_SourceStreamVariables__"></span><span id="_streamvariablelines__objref-_sourcestreamvariables__"></span><span id="_STREAMVARIABLELINES__OBJREF-_SOURCESTREAMVARIABLES__"></span><strong>@StreamVariableLines= $objref &gt; ( # B1 </strong>  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
使源代码管理系统可以将特定于源代码管理的变量添加到每个调试文件的源流中。 示例模块使用此方法来写入所需的提取 \_ CMD 并提取 \_ 目标变量。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**Parameters**  
无

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  

<span id="_StreamVariableLines"></span><span id="_streamvariablelines"></span><span id="_STREAMVARIABLELINES"></span><em>@StreamVariableLines</em>  
源流变量的条目列表。

 

 





