---
title: 匹配符号名称
description: 匹配符号名称
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 627a88040ac8505b7f1f92f150c78fba0d13720e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814531"
---
# <a name="matching-symbol-names"></a>匹配符号名称


在某些情况下，符号的实际名称将替换为替代形式，这会导致符号匹配问题。 当在公共和私有符号之间进行更改时，或者在使用 MS-DOS 兼容性8.3 文件的短名称时，通常会发生这种情况。

### <a name="span-idpublic_vs__private_symbol_matchingspanspan-idpublic_vs__private_symbol_matchingspanpublic-vs-private-symbol-matching"></a><span id="public_vs__private_symbol_matching"></span><span id="PUBLIC_VS__PRIVATE_SYMBOL_MATCHING"></span>Public 和 Private 符号匹配

在公共符号和私有符号之间切换有时会导致符号匹配问题。 通常，公共符号和对应的私有符号具有不同的符号修饰名称。 但在某些情况下，它们可能具有完全不同的名称。 在这种情况下，可能必须显式引用这两个名称。 例如，可以设置两个断点：一个在公共符号上，另一个位于私有符号上。 有关更多详细信息，请参阅 [公共和私有符号](public-and-private-symbols.md)。

### <a name="span-idms_dos_compatability_8_3_short_name_symbol_matchingspanspan-idms_dos_compatability_8_3_short_name_symbol_matchingspanms-dos-compatibility-83-short-name-symbol-matching"></a><span id="ms_dos_compatability_8_3_short_name_symbol_matching"></span><span id="MS_DOS_COMPATABILITY_8_3_SHORT_NAME_SYMBOL_MATCHING"></span>MS-DOS 兼容性8.3 短名称符号匹配

有时，具有非常长的名称的文件会被指定为自动生成的 MS-DOS 兼容性8.3 短名称。 根据用于创建符号文件和调试的工具和选项，存储在映像调试记录中的文件名可以是长名称，也可以是这些短名称之一。 如果使用短名称，则这可能会导致符号匹配问题，因为分配的短名称依赖于系统。

例如，假设有两个文件（Longfilename1 和 Longfilename2）。 如果将它们放在同一目录中，则会将 MS-DOS 兼容性8.3 的名称 Longfi ~ 1，另一个将为 Longfi ~ 2。 如果未将它们放在同一目录中，则它们将 Longfi ~ 1。 因此，如果将关联的 .pdb 文件复制到漫不经心，则短文件名可能会改变，从而导致符号匹配问题。 有关更多详细信息，请参阅 [文件系统引用和符号文件](file-system-references-and-symbol-files.md)。

 

 





