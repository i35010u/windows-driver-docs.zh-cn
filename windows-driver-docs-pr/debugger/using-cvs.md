---
title: 使用 CVS
description: 使用 CVS
ms.assetid: 4ad1202e-0be5-4adc-af8b-6b8d7cb34b04
keywords:
- 并发版本 System (CVS)
- 源服务器、 CVS
- SrcSrv, CVS
- 并发版本 System (CVS) 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e3a916e4bfc75dd7e68edc42c42fc0a4f2b555e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525566"
---
# <a name="using-cvs"></a>使用 CVS


源服务器的 CVS 模块是使用并发版本 System (CVS) 1.11.17 （客户端） 开发的。 未与任何其他版本的 CVS 经过测试它。 此外，该模块的当前版本为 beta 版本。

### <a name="span-idcvsrootspanspan-idcvsrootspancvsroot"></a><span id="cvsroot"></span><span id="CVSROOT"></span>CVSROOT

在计算机上的源索引生成，CVSROOT 不能包含密码和用户信息。 使用 cvs.exe 设置验证信息。

若要准备[Srcsrv.ini](the-srcsrv-ini-file.md)文件 CVS 索引，您必须输入你的存储库的唯一使它有别于网络中的其他别名。 此存储库必须与您的环境中的 CVSROOT 值匹配。 没有必要将此值设置在因为源索引的.pdb 文件中定义别名与调试器客户端保持的 Srcsrv.ini 的副本。

### <a name="span-idclientcomputerspanspan-idclientcomputerspanclient-computer"></a><span id="client_computer"></span><span id="CLIENT_COMPUTER"></span>客户端计算机

在调试过程中提取文件的客户端计算机不需要 CVS 沙盒或 CVSROOT 集。 它需要位于 CVS 二进制文件的路径中，如果存储库已锁定，则必须设置的用户名和密码与 Cvs.exe。

### <a name="span-idrevisiontagsspanspan-idrevisiontagsspanrevision-tags"></a><span id="revision_tags"></span><span id="REVISION_TAGS"></span>修订标记

CVS 不能提取其版本号的文件。 相反，必须完成使用什么通常所说*标记*。 当索引基于 CVS 的系统，必须确保所有更改签入存储库，并将使用"cvs 标记"命令的标记。 然后，当索引文件，确保"标签"命令行参数用于指定你想要将与创建索引的生成相关联的标记。 您可以设置 CVS 实现相同的结果\_在环境中的标签。 可以从该环境或命令行设置其他值。 使用 **-??** 命令行选项与 SSIndex 检查所做的选择，并验证所有已正确配置：

```console
ssindex.cmd -system=cvs -??
```

 

 





