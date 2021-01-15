---
title: Pvk2Pfx
description: 'Pvk2Pfx ( # A0) 是一个命令行工具，它将 .spc、.cer 和 pvk 文件中包含的公钥和私钥信息复制到个人信息交换 ( .pfx) 文件中。'
keywords:
- Pvk2Pfx 驱动程序开发工具
topic_type:
- apiref
api_name:
- Pvk2Pfx
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6c0e9303c681fddfa150c5675a7aa5ea207ed05
ms.sourcegitcommit: 5b7f2acb319287c5b255a7fe40c62606375cf31a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/15/2021
ms.locfileid: "98226555"
---
# <a name="pvk2pfx"></a>Pvk2Pfx


Pvk2Pfx ( # A0) 是一个命令行工具，它将 .spc、.cer 和 pvk 文件中包含的公钥和私钥信息复制到个人信息交换 ( .pfx) 文件中。

```
    pvk2pfx /pvk 
    pvkfilename.pvk [/pi pvkpassword] /spc spcfilename.ext [/pfx pfxfilename.pfx [/po pfxpassword] [/f]]
```

### <a name="span-idswitches_and_argumentsspanspan-idswitches_and_argumentsspanswitches-and-arguments"></a><span id="switches_and_arguments"></span><span id="SWITCHES_AND_ARGUMENTS"></span>开关和参数

<span id="_PVK_PVKFILENAME.PVK"></span>**/pvk** *pvkfilename. pvk*  
指定 pvk 文件的名称。

<span id="_SPC_SPCFILENAME.EXT"></span>**/spc** *spcfilename*  
指定包含证书的 [软件发行者证书 (SPC) ](../install/software-publisher-certificate.md) 文件的名称和扩展名。 该文件可以是 .spc 文件或 .cer 文件。

<span id="_PFX_PFXFILENAME.PFX"></span>**/pfx** *pfxfilename*  
指定 .pfx 文件的名称。

<span id="_pi_pvkpassword"></span><span id="_PI_PVKPASSWORD"></span>**/pi** *pvkpassword*  
指定 pvk 文件的密码。

<span id="_po_pfxpassword"></span><span id="_PO_PFXPASSWORD"></span>**/po** *pfxpassword*  
为 .pfx 文件指定密码。 如果未指定 .pfx 文件的密码，则该 .pfx 文件的密码将与 pvk 文件的密码相同。

<span id="_f"></span><span id="_F"></span>**/f**  
将 Pvk2Pfx 配置为覆盖 .pfx 文件（如果存在与 **-pfx** 开关指定的名称相同的文件）。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>备注

如果未提供 **-pfx** *pfxfilename* 开关，则 pvk2pfx 将忽略 **-po** *密码* 开关和 **-f** 开关，并显示一个向导，提示用户输入 .pfx 文件的名称及其对应的密码。

若要使用 [**SignTool**](signtool.md) 工具通过符合 [内核模式代码签名策略](../install/kernel-mode-code-signing-policy--windows-vista-and-later-.md)的方式对驱动程序进行签名，则必须将 SPC 信息添加到对驱动程序进行签名的本地计算机上的 "个人" 证书存储中。 有关如何向个人证书存储添加 SPC 信息的信息，请参阅 [软件发行者证书](../install/software-publisher-certificate.md)。

Pvk2Pfx 工具的32位版本位于 WDK 的 bin \\ x86 文件夹中。 此工具的64位版本位于 WDK 的 "bin" \\ x64。 例如，在运行 Windows 10 的基于 x64 的计算机上，路径为 C： \\ Program Files (x86) \\ Windows 工具包 \\ 10 \\ bin \\ x64。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面的命令从 Mypvkfile. pvk 和 Myspcfile 生成 .pfx 文件 Mypfxfile。 命令为 pvk 文件提供密码 mypassword，该文件将成为 .pfx 文件 Mypfxfile 的密码。 如果存在名为 Mypfxfile 的现有文件，则 **-f** 开关会将 Pvk2Pfx 工具配置为使用新文件替换现有文件。

```
pvk2pfx -pvk mypvkfile.pvk -pi mypassword -spc myspcfile.spc -pfx mypfxfile.pfx -f
```

 

