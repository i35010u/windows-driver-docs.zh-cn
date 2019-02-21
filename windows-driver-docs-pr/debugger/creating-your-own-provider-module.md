---
title: 创建你自己的提供程序模块
description: 创建你自己的提供程序模块
ms.assetid: 4282d375-bcf0-478f-bb2f-a43dc50b09e3
keywords:
- 版本控制系统，提供程序的模块
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a0ce3602ab4c46980e6892efdd539395a45059d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526970"
---
# <a name="creating-your-own-provider-module"></a>创建你自己的提供程序模块


一般情况下，若要创建你自己的提供程序模块，必须实现以下接口集。

<span id="_module__SimpleUsage__"></span><span id="_module__simpleusage__"></span><span id="_MODULE__SIMPLEUSAGE__"></span>**$module::SimpleUsage()**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
向 STDOUT 显示简单的模块使用情况信息。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**参数**  
无

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  
无

<span id="_module__VerboseUsage__"></span><span id="_module__verboseusage__"></span><span id="_MODULE__VERBOSEUSAGE__"></span>**$module::VerboseUsage()**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
向 STDOUT 显示深入模块使用情况信息。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**参数**  
无

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  
无

<span id="_objref____module__new__CommandArguments_"></span><span id="_objref____module__new__commandarguments_"></span><span id="_OBJREF____MODULE__NEW__COMMANDARGUMENTS_"></span>**$objref = $module::new(**<em>@CommandArguments</em>**)**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
初始化提供程序模块的实例。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**参数**  

<span id="_CommandArguments"></span><span id="_commandarguments"></span><span id="_COMMANDARGUMENTS"></span><em>@CommandArguments</em>  
所有@ARGV不被视为常规参数 ssindex.cmd 的参数。

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  
一个引用，可以在更高版本的操作中使用。

<span id="_objref-_GatherFileInformation__SourcePath__ServerHashReference_"></span><span id="_objref-_gatherfileinformation__sourcepath__serverhashreference_"></span><span id="_OBJREF-_GATHERFILEINFORMATION__SOURCEPATH__SERVERHASHREFERENCE_"></span>**$objref-&gt;GatherFileInformation(**<em>$SourcePath</em>**,**<em>$ServerHashReference</em>**)**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
使模块能够收集指定的目录所需的源索引编制信息 *$SourcePath*参数。 该模块不应假定仅在为每个对象 instancebecause SSIndex 可能会多次调用为不同的路径后，调用此项。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**参数**  

<span id="_SourcePath"></span><span id="_sourcepath"></span><span id="_SOURCEPATH"></span>*$SourcePath*  
包含要编制索引的源的本地目录。

<span id="_ServerHashReference"></span><span id="_serverhashreference"></span><span id="_SERVERHASHREFERENCE"></span>*$ServerHashReference*  
对包含所有指定的 Srcsrv.ini 文件中的项的哈希的引用。

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  
无

<span id="__VariableHashReference__FileEntry_____objref-_GetFileInfo__LocalFile_"></span><span id="__variablehashreference__fileentry_____objref-_getfileinfo__localfile_"></span><span id="__VARIABLEHASHREFERENCE__FILEENTRY_____OBJREF-_GETFILEINFO__LOCALFILE_"></span>**(**<em>$VariableHashReference</em>**,**<em>$FileEntry</em>**) = $objref**-&gt;**GetFileInfo(**<em>$LocalFile</em>**)**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
提供了必要的信息，从源代码管理系统中提取一个特定的文件。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**参数**  

<span id="_LocalFile"></span><span id="_localfile"></span><span id="_LOCALFILE"></span>*$LocalFile*  
完全限定的文件名。

<span id="Return_Values"></span><span id="return_values"></span><span id="RETURN_VALUES"></span>**返回值**  

<span id="_VariableHashReference"></span><span id="_variablehashreference"></span><span id="_VARIABLEHASHREFERENCE"></span>*$VariableHashReference*  
用于解释所返回的变量的哈希引用 *$FileEntry*。 Ssindex.cmd 缓存单个调试文件用于减少写入到源索引流信息的每个源文件这些变量。

<span id="_FileEntry"></span><span id="_fileentry"></span><span id="_FILEENTRY"></span>*$FileEntry*  
要写入到源索引流，以允许 SrcSrv 从源代码管理中提取此文件的文件条目。 此行的确切格式是特定于源代码管理系统。

<span id="_TextString___objref-_LongName__"></span><span id="_textstring___objref-_longname__"></span><span id="_TEXTSTRING___OBJREF-_LONGNAME__"></span><em>$TextString</em>**= $objref-&gt;LongName()**  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
提供的描述性字符串来标识向最终用户的源控制系统。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**参数**  
无

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  

<span id="_TextString"></span><span id="_textstring"></span><span id="_TEXTSTRING"></span>*$TextString*  
源代码管理系统的描述性名称。

<span id="_StreamVariableLines__objref-_SourceStreamVariables__"></span><span id="_streamvariablelines__objref-_sourcestreamvariables__"></span><span id="_STREAMVARIABLELINES__OBJREF-_SOURCESTREAMVARIABLES__"></span><strong>@StreamVariableLines=$objref-&gt;SourceStreamVariables()</strong>  

<span id="Purpose"></span><span id="purpose"></span><span id="PURPOSE"></span>**用途**  
启用源代码管理系统，可以将特定于控件的源的变量添加到每个调试文件的源流。 示例模块使用此方法用于写入需要的提取\_CMD 和提取\_目标变量。

<span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>**参数**  
无

<span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>**返回值**  

<span id="_StreamVariableLines"></span><span id="_streamvariablelines"></span><span id="_STREAMVARIABLELINES"></span><em>@StreamVariableLines</em>  
条目源流变量的列表。

 

 





