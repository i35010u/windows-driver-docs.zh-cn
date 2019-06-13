---
ms.assetid: bf92ab5f-9e54-4faa-8ae9-5cbe43434514
title: 签署驱动程序
description: 必须先签署所有在 64 位版本 Windows 上运行的驱动程序，然后 Windows 才会加载它们。 但是，在 32 位版本的 Windows.Visual Studio 上，无需签署驱动程序即可签署驱动程序包。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af4e7e65df105ae2951d5ad9165552efb68250db
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "64368648"
---
# <a name="signing-a-driver"></a>签署驱动程序

必须先签署所有在 64 位版本 Windows 上运行的驱动程序，然后 Windows 才会加载它们。 但是，32 位版本的 Windows 无需签署驱动程序。

若要签署驱动程序，则必须使用证书。 你可以创建自己的证书，以便在开发和测试过程中签署驱动程序。 但是，对于公开发布，你必须使用受信任的根证书颁发机构颁发的证书签署驱动程序。

**注意**  *驱动程序包项目*可以将其他项目的输出打包。 如果生成驱动程序包项目，则 Microsoft Visual Studio 将生成它所依赖的其他项目。 驱动程序包项目具有其自己的、与任何其他依赖项目分离的驱动程序签名属性，并且其驱动程序签名属性*仅*适用于该驱动程序包项目生成的目录（如果有）。 也就是说，驱动程序包项目不会将嵌入式签名自动添加到其他项目生成的驱动程序二进制文件中，因为可使用不同的证书来签署其他驱动程序项目，例如测试证书，此情况下的结果是该驱动程序包中的二进制文件使用一个证书意外签署，而程序包目录则使用另一个证书签署。 这可能会导致性能下降。 例如，如果某个引导启动驱动程序二进制文件的嵌入式签名无效，则 Windows 将无法使用其签署的证书来验证该二进制文件。 而是，Windows 必须根据目录的签名来验证该二进制文件，这就会增加启动时间。

 

本部分介绍了如何使用 Visual Studio 签署驱动程序包。

-   [在开发和测试期间签署驱动程序](signing-a-driver-during-development-and-testing.md)
-   [签署驱动程序以便公开发布](signing-a-driver-for-public-release.md)

 

 





