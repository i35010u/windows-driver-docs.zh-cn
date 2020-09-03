---
title: XpsConverter
description: 'XPS 转换器 ( # A0) 是一个命令行工具，用于将 XML 纸张规格 (XPS) 文档从 Microsoft XPS (MSXPS) 转换为标准 OpenXPS。'
ms.assetid: A51F818E-AECD-4EBD-99AC-F3BD026C19D6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0f829afab3d976464a36a61aa151aebf9bbeb50
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384259"
---
# <a name="xpsconverter"></a>XpsConverter


XPS 转换器 ( # A0) 是一个命令行工具，用于将 XML 纸张规格 (XPS) 文档从 Microsoft XPS (MSXPS) 转换为标准化 OpenXPS，从 OpenXPS 转换为 Microsoft XPS (MSXPS) 。 此工具旨在助手从一种 XPS 格式转换到另一种 XPS 格式。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在哪里可以下载 XpsConverter？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>XpsConverter.exe 包含在 Microsoft Windows 驱动程序工具包 (WDK) 中。 有关获取 WDK 的信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk" data-raw-source="[Windows Driver Kit Downloads](../download-the-wdk.md)">Windows 驱动程序工具包下载</a>。</p></td>
</tr>
</tbody>
</table>

 

与独立工具相比，XpsConverter 不应在任何其他容量中使用。 不支持使用此方法。 它不能在任何应用程序或驱动程序的部分或全部中使用，严格禁止取消编译或修改该工具。 Microsoft 保留所有权利，并保存有关 XpsConverter.exe 及其所有支持文档的版权。

**转换 XPS 文档**

1.  打开 Visual Studio 命令提示符窗口。

2.  运行 **XpsConverter.exe** 工具，并指定源和目标文件或文件夹的名称，并指定将文件 () 转换为的格式。

    例如，下面的命令将名为 MSXPS 的文件转换为 OpenXPS 格式。

    ```
    XpsConverter /OpenXPS /InputFile=Text.xps /OutputFile=Test.oxps
    ```

    安装 WDK 时，XpsConverter.exe 文件位于% programfiles% \\ Windows 工具包 \\ 8.1 \\ \\ * &lt; &gt; * bin 或% programfiles (86 \\ \\ \\ \\ * &lt; &gt; *) % windows 工具包 8.1 bin 目录。

## <a name="span-idxpsconverter_command_syntaxspanspan-idxpsconverter_command_syntaxspanspan-idxpsconverter_command_syntaxspanxpsconverter-command-syntax"></a><span id="XpsConverter_Command_Syntax"></span><span id="xpsconverter_command_syntax"></span><span id="XPSCONVERTER_COMMAND_SYNTAX"></span>XpsConverter 命令语法


```
  XpsConverter  <format>  
  [/InputFile=<inputfile> /OutputFile=<outputfile>  | /InputFolder=<inputfolder> /OutputFolder=<outputfolder>]  

  [-logger:<LoggerType>]
  [-logfile:<LogFile>  ]
  [ -device:<DeviceString> ]
  [ /? ]
```

## <a name="span-idcommand_parametersspanspan-idcommand_parametersspanspan-idcommand_parametersspancommand-parameters"></a><span id="Command_parameters"></span><span id="command_parameters"></span><span id="COMMAND_PARAMETERS"></span>命令参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_format_"></span><span id="_FORMAT_"></span><em>&lt;形式&gt;</em></p></td>
<td align="left"><p>指定将)  (的源文件转换为的格式。 <em> &lt; 格式 &gt; </em>是必需的。 指定 <strong>/OpenXPS</strong> 以将文档)  (s 转换为 OpenXPS 或 <strong>/XPS</strong> ，以将文档)  (s 转换为 Microsoft XPS (MSXPS) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_InputFile__inputfile___OutputFile__outputfile_"></span><span id="_inputfile__inputfile___outputfile__outputfile_"></span><span id="_INPUTFILE__INPUTFILE___OUTPUTFILE__OUTPUTFILE_"></span><strong>/InputFile =</strong><em> &lt; InputFile &gt; </em> <strong>/outputfile =</strong><em> &lt; OutputFile &gt; </em></p></td>
<td align="left"><p>使用此选项可转换<em> &lt; inputfile &gt; </em>并将其保存到<em> &lt; outputfile &gt; </em>。 <em> &lt; Inputfile &gt; </em>必须具有 .xps 或 .oxps 文件扩展名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_InputFolder__inputfolder____OutputFolder__outputfolder_"></span><span id="_inputfolder__inputfolder____outputfolder__outputfolder_"></span><span id="_INPUTFOLDER__INPUTFOLDER____OUTPUTFOLDER__OUTPUTFOLDER_"></span><strong>/InputFolder =</strong><em> &lt; InputFolder &gt; </em> <strong>/OutputFolder =</strong><em> &lt; OutputFolder &gt; </em></p></td>
<td align="left"><p>使用此选项可转换<em> &lt; inputfolder &gt; </em>中的所有文件，并将其保存到<em> &lt; outputfolder &gt; </em>。 <em> &lt; Inputfolder &gt; </em>中的文件必须具有 .xps 或 .oxps 文件扩展名。</p>
<div class="alert">
<strong>注意</strong>   转换文件夹是一个递归操作。 该工具会转换指定的<em> &lt; inputfolder &gt; </em>和所有子目录中的所有文件。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><span id="__-logger__LoggerType_"></span><span id="__-logger__loggertype_"></span><span id="__-LOGGER__LOGGERTYPE_"></span><strong>-记录器：</strong><em> &lt; LoggerType &gt; </em></p></td>
<td align="left"><p>可选。 <em> &lt; LoggerType &gt; </em>指示在转换期间要使用 (<strong>文件</strong>、<strong>控制台</strong>或<strong>WTT</strong>) 生成的日志类型。 默认记录器为 <strong>控制台</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="-logfile__LogFile_"></span><span id="-logfile__logfile_"></span><span id="-LOGFILE__LOGFILE_"></span><strong>-logfile：</strong><em> &lt; 日志 &gt; 文件</em></p></td>
<td align="left"><p>可选。 指定<strong>-记录器</strong>选项为<strong>FILE</strong>时要使用的<em> &lt; &gt; 日志</em>文件。 如果未指定<em> &lt; 日志 &gt; </em>文件，则 XpsConverter.txt 默认的日志文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="-device__DeviceString_"></span><span id="-device__devicestring_"></span><span id="-DEVICE__DEVICESTRING_"></span><strong>-device：</strong><em> &lt; DeviceString &gt; </em></p></td>
<td align="left"><p>可选。 指定在<strong>-记录器</strong>选项为<strong>WTT</strong>时要使用的<em> &lt; &gt; DeviceString</em> 。 默认设备是 <strong>$LogFile： file = XpsConverter，wtl，WriteMode = append</strong>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


你可以使用 **isXPS.exe (Isxps.exe 一致性工具) ** 来测试文件对 XPS 的符合性，以及 (OPC) 规范的开放打包约定。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


```
XpsConverter /OpenXPS /InputFile=Text.xps /OutputFile=Test.oxps
XpsConverter /XPS /InputFolder=c:\OpenXPS /OutputFolder=c:\MSXPS
XpsConverter /OpenXPS /InputFile=MyDoc.xps /OutputFile=ConvertedMyDoc.oxps  logger:file  logfile:MyLog.txt
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


**isXPS.exe（isXPS 合规性工具）**

 

