---
title: 使用源文件
description: 使用源文件
keywords:
- 调试器引擎 API，源
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86471aa513e2ab79feebb8859521380bcf1776ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803065"
---
# <a name="using-source-files"></a>使用源文件


[调试器引擎](introduction.md#debugger-engine)维护 *源路径*，该路径是包含与当前目标关联的源代码文件的目录和源服务器的列表。 调试器引擎可以在这些目录和源服务器中搜索源文件。 在符号文件的帮助下，调试器引擎可以将源文件中的行与目标内存中的位置匹配。

有关将源文件用于调试器的概述，请参阅 [在源模式下进行调试](debugging-in-source-mode.md)。 有关源路径的概述，请参阅 [源路径](source-path.md)。 有关从调试器引擎使用源服务器的概述，请参阅 [使用源服务器](using-a-source-server.md)。

### <a name="span-idsource_pathspanspan-idsource_pathspansource-path"></a><span id="source_path"></span><span id="SOURCE_PATH"></span>源路径

若要将目录或源服务器添加到源路径，请使用方法 [**AppendSourcePath**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-appendsourcepath)。 整个源路径由 [**GetSourcePath**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsourcepath) 返回，可使用 [**SetSourcePath**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setsourcepath)进行更改。 可以使用 [**GetSourcePathElement**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsourcepathelement)从源路径中检索单个目录或源服务器。

若要查找与源路径相关的源文件，请使用 [**FindSourceFile**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-findsourcefile) 或，有关使用源服务器时的更高级选项，请使用 [**FindSourceFileAndToken**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-findsourcefileandtoken)。 **FindSourceFileAndToken** 还可以与 [**GetSourceFileInformation**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-getsourcefileinformation) 一起使用，以检索与源服务器上的文件相关的变量。

### <a name="span-idmatching_source_files_to_code_in_memoryspanspan-idmatching_source_files_to_code_in_memoryspanmatching-source-files-to-code-in-memory"></a><span id="matching_source_files_to_code_in_memory"></span><span id="MATCHING_SOURCE_FILES_TO_CODE_IN_MEMORY"></span>将源文件与内存中的代码匹配

调试器引擎提供了三种方法来查找与源文件中的行相对应的内存位置。 若要将一行源代码映射到内存位置，请使用 [**GetOffsetByLine**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getoffsetbyline)。 若要在内存位置中搜索多个源行或附近的源行，请使用 [**GetSourceEntriesByLine**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsourceentriesbyline)。 [**GetSourceFileLineOffsets**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsourcefilelineoffsets)方法将返回源文件中每行的内存位置。

若要执行相反的操作并查找与目标内存中某个位置相匹配的源文件的行，请使用 [**GetLineByOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getlinebyoffset)。

**注意**  源文件中的内存位置与行之间的关系不一定是一对一关系。 单行源代码可以与多个内存位置对应，而单个内存位置则对应于多行源代码。

 

 

