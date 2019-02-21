---
title: 卡的要求
description: 卡的要求
ms.assetid: 3BE887F9-4B35-4A83-9E98-DD7555DF2953
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c46911e0aa0fe77815b353f52e3e44ec665d00f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523225"
---
# <a name="card-requirements"></a>卡的要求


要为其他要求提供一些背景信息，本部分提供有关如何预配和使用卡一些信息。

## <a name="span-idwhatablankcardisspanspan-idwhatablankcardisspanspan-idwhatablankcardisspanwhat-a-blank-card-is"></a><span id="What_a__Blank_Card__Is"></span><span id="what_a__blank_card__is"></span><span id="WHAT_A__BLANK_CARD__IS"></span>什么是"Blank 卡"


"空白卡，"该值可进行"创建"，然后使用由 Microsoft 智能卡基本 CSP/KSP，是一种卡的：

-   包含卡操作系统。
-   包含或可以虚拟化必要的文件和数据以实现文件系统。
-   具有默认值为管理和/或用户的 Pin 或密钥。
-   还没有讨论"卡创建"（下一节） 下的文件。
-   尚无更多的准备工作的卡创建。
-   对于将来的目的，可以提供帮助 ISO 7816-4 第 8 部分中定义。

## <a name="span-idcardcreationspanspan-idcardcreationspanspan-idcardcreationspan-card-creation"></a><span id="_Card__Creation_"></span><span id="_card__creation_"></span><span id="_CARD__CREATION_"></span> 卡"创建"


卡片可用于加密操作来说，它必须具有一个标识，使它可以识别部署和管理，并且它必须是可用的基本 CSP/KSP。 这需要卡 ID 文件和存储在卡上所需的基本 CSP/KSP 某些文件。 创建这些必要的文件在卡上的操作称为"创建"卡。 这通过部署工具，包括以下步骤：

1.  创建与每个人都具有读取和拥有写入权限的管理员卡 ID 文件，"cardid"卡的根目录中。 此文件包含在卡的唯一的 16 字节二进制标识符。 它永远不会更新或覆盖，除非卡是完全回收。
2.  与具有读/写权限的所有人创建的缓存文件，"cardcf"的根目录中。 初始的内容是值为零的 6 个字节。
3.  与每个人都具有读取和拥有写入权限的用户创建应用程序映射"cardapps"的根目录中。 初始的内容是一个 8 字节记录，其中包含字符串"mscp"跟 4 零字节。
4.  创建基本 CSP CNG/KSP 应用程序通过调用[ **CardCreateDirectory**](https://msdn.microsoft.com/library/windows/hardware/dn468710)、 引用应用程序"mscp"、 与每个人都具有读取和用户拥有写入权限。
5.  在与每个人都具有读取和写入权限的用户的"mscp"目录中创建证书映射文件中，"cmapfile"。 它是最初为空。

从技术上讲，卡"创建"后步骤 2，但我们定义所有卡应都保留 Microsoft"mscp"应用程序，不管是实际使用。 本部分说明异常的事实，始终创建"mscp"应用程序和"mscp"应用程序中创建一个文件。 按预期方式卡创建由卡管理 Microsoft 提供的 DLL 中的函数来实现，提供此信息作为卡微型驱动程序作者能够正确地支持这些操作在该上下文中的参考信息。

 

 





