---
title: 使用 CVS
description: 使用 CVS
keywords:
- '并发版本系统 (CVS) '
- 源服务器，CVS
- Srcsrv.ini，CVS
- 并发版本系统 (CVS) ，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86265704986546d4981293180cfe901dad51d4b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803151"
---
# <a name="using-cvs"></a>使用 CVS


源服务器的 CVS 模块是使用并发版本系统 (CVS) 1.11.17 (客户端) 开发的。 尚未通过任何其他版本的 CVS 对其进行测试。 而且，模块的当前版本是 beta 版本。

### <a name="span-idcvsrootspanspan-idcvsrootspancvsroot"></a><span id="cvsroot"></span><span id="CVSROOT"></span>CVSROOT

在源构建索引的计算机上，CVSROOT 不能包含密码和用户信息。 使用 cvs.exe 设置 credentialing 信息。

若要为 CVS 索引准备 [Srcsrv.ini](the-srcsrv-ini-file.md) 文件，必须为存储库输入一个别名，以便将其与网络中的其他任何人区分开来。 此存储库必须与您的环境中的 CVSROOT 值匹配。 不需要在与调试器客户端保留的 Srcsrv.ini 副本中设置此值，因为别名是在源索引 .pdb 文件中定义的。

### <a name="span-idclient_computerspanspan-idclient_computerspanclient-computer"></a><span id="client_computer"></span><span id="CLIENT_COMPUTER"></span>客户端计算机

在调试过程中提取文件的客户端计算机不需要 CVS 沙盒或 CVSROOT 集。 它在路径中需要 CVS 二进制文件，如果存储库已锁定，则必须 Cvs.exe 设置用户名和密码。

### <a name="span-idrevision_tagsspanspan-idrevision_tagsspanrevision-tags"></a><span id="revision_tags"></span><span id="REVISION_TAGS"></span>修订标记

CVS 无法按文件版本号提取文件。 相反，必须使用所谓的 *标记* 完成此操作。 对基于 CVS 的系统进行索引时，必须确保将所有更改签入到存储库，然后使用 "CVS 标记" 命令应用标记。 然后，在对文件进行索引时，请确保使用 "标签" 命令行参数来指定要与要编制索引的生成关联的标记。 您可以通过在环境中设置 CVS 标签获得相同的结果 \_ 。 可以从环境或命令行设置其他值。 使用 **-??** 带有 Ssindex.cmd 的命令行选项，用于检查你的选择并验证是否已正确配置所有内容：

```console
ssindex.cmd -system=cvs -??
```

 

 





