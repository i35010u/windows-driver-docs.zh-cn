---
title: XpsConverter
description: XPS 转换器 (XpsConverter.exe) 是用于将 XML 纸张规范 (XPS) 文档从 Microsoft XPS (MSXPS) 转换为标准化 OpenXPS 的命令行工具。
ms.assetid: A51F818E-AECD-4EBD-99AC-F3BD026C19D6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b974e968a6f8967ff1c79c4c304f0834f7bc9a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564942"
---
# <a name="xpsconverter"></a>XpsConverter


XPS 转换器 (XpsConverter.exe) 是一个命令行工具从 Microsoft XPS (MSXPS) 到标准化 OpenXPS，以及从 OpenXPS 到 Microsoft XPS (MSXPS) 转换为 XML 纸张规范 (XPS) 文档。 此工具从到另一种 XPS 格式适用于以下助手 XPS 测试附件在转换中。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在何处可以下载 XpsConverter？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>XpsConverter.exe 包含 Microsoft Windows Driver Kit (WDK) 中。 有关获取 WDK 的信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=290798" data-raw-source="[Windows Driver Kit Downloads]( https://go.microsoft.com/fwlink/p/?linkid=290798)">Windows 驱动程序工具包下载</a>。</p></td>
</tr>
</tbody>
</table>

 

XpsConverter 不是要在中比任何其他容量作为独立工具使用。 不支持任何其他用途。 它不能使用部分或完全禁止在任何应用程序或驱动程序和反编译或修改该工具的整体。 Microsoft 保留所有权限，并保留版权 XpsConverter.exe 和其支持的所有文档。

**若要将 XPS 文档转换**

1.  打开 Visual Studio 命令提示符窗口。

2.  运行**XpsConverter.exe**工具和指定的源和目标文件或文件夹的名称，然后指定要转换到的文件的格式。

    例如，以下命令将名为 OpenXPS 格式 text.xps MSXPS 文件转换。

    ```
    XpsConverter /OpenXPS /InputFile=Text.xps /OutputFile=Test.oxps
    ```

    在安装 WDK 时，XpsConverter.exe 文件位于 %programfiles%\\Windows 工具包\\8.1\\bin\\*&lt;arch&gt;* 或 %programfiles(86) %\\Windows 工具包\\8.1\\bin\\*&lt;arch&gt;* 目录。

## <a name="span-idxpsconvertercommandsyntaxspanspan-idxpsconvertercommandsyntaxspanspan-idxpsconvertercommandsyntaxspanxpsconverter-command-syntax"></a><span id="XpsConverter_Command_Syntax"></span><span id="xpsconverter_command_syntax"></span><span id="XPSCONVERTER_COMMAND_SYNTAX"></span>XpsConverter 命令语法


```
  XpsConverter  <format>  
  [/InputFile=<inputfile> /OutputFile=<outputfile>  | /InputFolder=<inputfolder> /OutputFolder=<outputfolder>]  

  [-logger:<LoggerType>]
  [-logfile:<LogFile>  ]
  [ -device:<DeviceString> ]
  [ /? ]
```

## <a name="span-idcommandparametersspanspan-idcommandparametersspanspan-idcommandparametersspancommand-parameters"></a><span id="Command_parameters"></span><span id="command_parameters"></span><span id="COMMAND_PARAMETERS"></span>命令参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_format_"></span><span id="_FORMAT_"></span><em>&lt;format&gt;</em></p></td>
<td align="left"><p>指定要转换到源文件的格式。 <em>&lt;格式&gt;</em>是必需的。 指定<strong>/OpenXPS</strong>若要将文档转换为 OpenXPS 或<strong>/XPS</strong>要转换到 Microsoft XPS (MSXPS) 的文档。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="_InputFile__inputfile___OutputFile__outputfile_"></span><span id="_inputfile__inputfile___outputfile__outputfile_"></span><span id="_INPUTFILE__INPUTFILE___OUTPUTFILE__OUTPUTFILE_"></span><strong>/InputFile=</strong><em>&lt;inputfile&gt;</em> <strong>/OutputFile=</strong><em>&lt;outputfile&gt;</em></p></td>
<td align="left"><p>使用此选项可将转换<em>&lt;inputfile&gt;</em>并将其保存到 <em>&lt;outputfile&gt;</em>。 <em>&lt;Inputfile&gt;</em>必须具有.xps 或.oxps 文件扩展名。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="_InputFolder__inputfolder____OutputFolder__outputfolder_"></span><span id="_inputfolder__inputfolder____outputfolder__outputfolder_"></span><span id="_INPUTFOLDER__INPUTFOLDER____OUTPUTFOLDER__OUTPUTFOLDER_"></span><strong>/InputFolder=</strong><em>&lt;inputfolder&gt;</em> <strong>/OutputFolder=</strong><em>&lt;outputfolder&gt;</em></p></td>
<td align="left"><p>使用此选项可将转换中的所有文件<em>&lt;inputfolder&gt;</em>并将它们到保存 <em>&lt;outputfolder&gt;</em>。 中的文件<em>&lt;inputfolder&gt;</em>必须具有.xps 或.oxps 文件扩展名。</p>
<div class="alert">
<strong>请注意</strong>将文件夹转换为递归操作。 该工具将所有文件中指定的 s 都转换<em>&lt;inputfolder&gt;</em> 及所有子目录。
</div>
<div>
 
</div></td>
</tr>
<tr class="even">
<td align="left"><p><span id="__-logger__LoggerType_"></span><span id="__-logger__loggertype_"></span><span id="__-LOGGER__LOGGERTYPE_"></span> <strong>-logger:</strong><em>&lt;LoggerType&gt;</em></p></td>
<td align="left"><p>可选。 <em>&lt;LoggerType&gt;</em> 指示要生成日志的类型 (<strong>文件</strong>，<strong>控制台</strong>或者<strong>WTT</strong>) 若要在转换过程中使用。 默认记录器是<strong>控制台</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="-logfile__LogFile_"></span><span id="-logfile__logfile_"></span><span id="-LOGFILE__LOGFILE_"></span><strong>-logfile:</strong><em>&lt;LogFile&gt;</em></p></td>
<td align="left"><p>可选。 指定<em>&lt;日志文件&gt;</em>时要使用<strong>-记录器</strong>选项<strong>文件</strong>。 如果未指定<em>&lt;日志文件&gt;</em>的默认日志文件是 XpsConverter.txt。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="-device__DeviceString_"></span><span id="-device__devicestring_"></span><span id="-DEVICE__DEVICESTRING_"></span><strong>-device:</strong><em>&lt;DeviceString&gt;</em></p></td>
<td align="left"><p>可选。 指定<em>&lt;DeviceString&gt;</em> 时要使用<strong>-记录器</strong>选项<strong>WTT</strong>。 默认设备是<strong>$LogFile:file=XpsConverter.wtl,WriteMode=append</strong>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


可以使用**isXPS.exe （isxps 合规性工具）** 到测试到 XPS 和开放打包约定 (OPC) 规范的文件的符合性。

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例


```
XpsConverter /OpenXPS /InputFile=Text.xps /OutputFile=Test.oxps
XpsConverter /XPS /InputFolder=c:\OpenXPS /OutputFolder=c:\MSXPS
XpsConverter /OpenXPS /InputFile=MyDoc.xps /OutputFile=ConvertedMyDoc.oxps  logger:file  logfile:MyLog.txt
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


**isXPS.exe （isxps 合规性工具）**

 

 






