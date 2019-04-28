---
title: Pvk2Pfx
description: Pvk2Pfx (Pvk2Pfx.exe) 是一个命令行工具将公钥和私钥信息包含在.spc、.cer 中，并.pvk 文件复制到个人信息交换 (.pfx) 文件中。
ms.assetid: f3fb3703-0e33-4d7f-b2ad-52bc035e01de
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
ms.openlocfilehash: 3e0a35557cca9be560c18d8b359b88a585edd4d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346987"
---
# <a name="pvk2pfx"></a>Pvk2Pfx


Pvk2Pfx (Pvk2Pfx.exe) 是一个命令行工具将公钥和私钥信息包含在.spc、.cer 中，并.pvk 文件复制到个人信息交换 (.pfx) 文件中。

```
    pvk2pfx /pvk 
    pvkfilename.pvk [/pi pvkpassword] /spc spcfilename.ext [/pfx pfxfilename.pfx [/po pfxpassword] [/f]]
```

### <a name="span-idswitchesandargumentsspanspan-idswitchesandargumentsspanswitches-and-arguments"></a><span id="switches_and_arguments"></span><span id="SWITCHES_AND_ARGUMENTS"></span>开关和参数

<span id="_PVK_PVKFILENAME.PVK"></span>**/pvk** *pvkfilename.pvk*  
指定一个.pvk 文件的名称。

<span id="_SPC_SPCFILENAME.EXT"></span>**/spc** *spcfilename.ext*  
指定的名称和扩展名[软件发布者证书 (SPC)](https://msdn.microsoft.com/library/windows/hardware/ff552299)包含证书的文件。 该文件可以是.spc 文件或.cer 文件。

<span id="_PFX_PFXFILENAME.PFX"></span>**/pfx** *pfxfilename.pfx*  
指定.pfx 文件的名称。

<span id="_pi_pvkpassword"></span><span id="_PI_PVKPASSWORD"></span>**/pi** *pvkpassword*  
指定.pvk 文件的密码。

<span id="_po_pfxpassword"></span><span id="_PO_PFXPASSWORD"></span>**/po** *pfxpassword*  
指定.pfx 文件的密码。 如果未指定.pfx 文件的密码，.pfx 文件的密码将作为.pvk 文件的密码相同。

<span id="_f"></span><span id="_F"></span>**/f**  
配置 Pvk2Pfx 覆盖.pfx 文件，如果存在与指定的同名 **-pfx**切换。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

如果 **-pfx** *pfxfilename.pfx*不提供开关、 pvk2pfx 忽略**po** *密码*切换和 **-f**切换，并显示一个向导，将提示用户输入.pfx 文件和其对应的密码的名称。

若要使用[ **SignTool** ](signtool.md)工具来签署驱动程序符合的方式使用 SPC[内核模式代码签署策略](https://msdn.microsoft.com/library/windows/hardware/ff548231)，必须将 SPC 信息添加到对进行签名的驱动程序在本地计算机上个人证书存储。 有关如何将 SPC 信息添加到个人证书存储区的信息，请参阅[软件发布者证书](https://msdn.microsoft.com/library/windows/hardware/ff552299)。

Pvk2Pfx 工具的 32 位版本位于 bin\\x86 WDK 的文件夹。 该工具的 64 位版本位于 bin\\x64 版本的 WDK。 例如，在基于 x64 的计算机上运行 Windows 10，路径为 c:\\Program Files (x86)\\Windows 工具包\\10\\bin\\x64。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>示例

下面的命令生成.pfx 文件 Mypfxfile.pfx 从 Mypvkfile.pvk 和 Myspcfile.spc。 该命令提供.pvk 文件，则将其转换为.pfx 文件 Mypfxfile.pfx 密码密码 mypassword。 如果没有名为 Mypfxfile.pfx，现有的文件 **-f**开关配置 Pvk2Pfx 工具用新文件替换现有文件。

```
pvk2pfx -pvk mypvkfile.pvk -pi mypassword -spc myspcfile.spc -pfx mypfxfile.pfx -f
```

 

 





