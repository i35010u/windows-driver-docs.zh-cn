---
title: 卡要求
description: 卡要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d16dd3e67d64020b802583ca6e7d6cddf51107cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811929"
---
# <a name="card-requirements"></a>卡要求


若要为其他要求提供某些上下文，本部分提供了有关如何设置和使用卡的一些信息。

## <a name="span-idwhat_a__blank_card__isspanspan-idwhat_a__blank_card__isspanspan-idwhat_a__blank_card__isspanwhat-a-blank-card-is"></a><span id="What_a__Blank_Card__Is"></span><span id="what_a__blank_card__is"></span><span id="WHAT_A__BLANK_CARD__IS"></span>什么是 "空白卡"


"空白卡"，可以 "创建" 后由 Microsoft 智能卡基本 CSP/KSP 使用，它是一个卡：

-   包含卡操作系统。
-   包含或可以虚拟化必要的文件和数据以实现文件系统。
-   为管理和/或用户 Pin 或密钥提供默认值。
-   还没有在 "创建卡" 下讨论的文件 (以下部分) 。
-   已准备好创建卡，无需进一步准备。
-   出于将来的目的，可以提供 ISO 7816-4 第8部分定义的帮助。

## <a name="span-id_card__creation_spanspan-id_card__creation_spanspan-id_card__creation_span-card-creation"></a><span id="_Card__Creation_"></span><span id="_card__creation_"></span><span id="_CARD__CREATION_"></span> 卡 "创建"


为了使卡对加密操作非常有用，它必须具有一个标识，使其能够被识别，以便进行部署和管理，并且它必须可供基本 CSP/KSP 使用。 这需要一个卡 ID 文件和基本 CSP/KSP 需要在卡上存储的某些文件。 在卡上创建这些所需文件的操作称为 "创建" 卡。 这是通过部署工具来完成的，其中包括以下步骤：

1.  在卡的根目录中创建卡 ID 文件 "cardid"，其中包含具有读取权限的所有人和具有写入权限的管理员。 此文件包含卡的唯一16字节二进制标识符。 除非完全回收卡，否则永远不会对其进行更新或覆盖。
2.  在根目录中创建缓存文件 "cardcf"，其中每个用户具有读/写权限。 初始内容为6个字节，其值为零。
3.  在根目录中创建应用程序映射 "cardapps"，其中包含具有 "写入" 权限的 "读取" 和 "用户"。 初始内容是一个8字节记录，其中包含字符串 "mscp" 后跟4个零字节。
4.  通过调用 [**CardCreateDirectory**](/previous-versions/dn468710(v=vs.85))来创建基本 CSP/CNG KSP 应用程序，该应用程序引用应用程序 "mscp"，每个人都具有写入权限。
5.  在 "mscp" 目录中创建证书映射文件 "cmapfile"，其中每个用户都具有写入权限。 它最初为空。

从技术上说，卡片在步骤2之后是 "创建" 的，但我们定义所有卡都应保留 Microsoft "mscp" 应用程序，而不管它是否确实使用。 这说明了始终创建 "mscp" 应用程序以及在 "mscp" 应用程序中创建文件的异常事实。 由于智能卡创建应由 Microsoft 提供的卡管理 DLL 中的函数来实现，因此此信息作为卡微型驱动程序作者的参考信息提供，以便能够在该上下文中正确支持这些操作。

 

