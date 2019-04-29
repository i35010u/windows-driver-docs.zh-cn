---
title: 匹配符号名称
description: 匹配符号名称
ms.assetid: 34e2401e-9074-4adc-9644-48ad768c7c2f
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ec0923b8195cba2142965c877a8d3302c4ade84
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353941"
---
# <a name="matching-symbol-names"></a>匹配符号名称


在某些情况下，一个符号的实际名称将被替换的替代形式，这则可能会导致符号匹配问题。 这通常发生在公共和私有符号之间的更改或使用 MS-DOS 兼容性 8.3 短名称的文件时。

### <a name="span-idpublicvsprivatesymbolmatchingspanspan-idpublicvsprivatesymbolmatchingspanpublic-vs-private-symbol-matching"></a><span id="public_vs__private_symbol_matching"></span><span id="PUBLIC_VS__PRIVATE_SYMBOL_MATCHING"></span>公共 vs。匹配的私有符号

公共符号和私有符号之间切换有时会导致符号匹配问题。 通常情况下，公共符号和相应的私有符号具有不同符号修饰名称相同。 但在某些情况下，它们可能具有完全不同的名称。 在这种情况下，可能需要显式引用这两个名称。 例如，可以设置两个断点： 一个在公共符号，，第二个私有符号。 有关更多详细信息，请参阅[公共和私有符号](public-and-private-symbols.md)。

### <a name="span-idmsdoscompatability83shortnamesymbolmatchingspanspan-idmsdoscompatability83shortnamesymbolmatchingspanms-dos-compatibility-83-short-name-symbol-matching"></a><span id="ms_dos_compatability_8_3_short_name_symbol_matching"></span><span id="MS_DOS_COMPATABILITY_8_3_SHORT_NAME_SYMBOL_MATCHING"></span>MS-DOS 兼容性 8.3 短名称匹配的符号

文件具有很长的名称有时可以自动生成 MS-DOS 兼容性 8.3 短名称。 根据的工具和选项用于创建符号文件和调试，图像的调试记录中存储的文件名称可以是长名称或其中一个短名称。 如果使用短名称，则这会导致符号取决于系统分配的短名称匹配的问题。

例如，假设有两个文件，Longfilename1.pdb 和 Longfilename2.pdb。 如果将它们放一个将相同的目录中具有 Longfi~1.pdb MS-DOS 兼容性 8.3 名称和另一个将是 Longfi~2.pdb。 如果它们不放在同一目录中它们都将 Longfi~1.pdb。 因此，如果不复制关联的.pdb 文件，可以更改短文件名，从而导致匹配的问题的符号。 有关更多详细信息，请参阅[文件系统引用和符号文件](file-system-references-and-symbol-files.md)。

 

 





