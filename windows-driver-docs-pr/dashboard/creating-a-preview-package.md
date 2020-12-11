---
title: 创建预览程序包
description: 创建预览程序包
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd8b2db223200dcb21107ef3d201fa55e63931c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800389"
---
# <a name="creating-a-preview-package"></a>创建预览程序包

当你创建预览包时，你可以提交它仅用于预览。 这让你能够在客户端设备上测试体验，然后更改或修改该体验，之后将它发布为实时体验。

## <a name="submitting-a-preview-package"></a>提交预览包

在提交预览包之前，你必须首先创建你的公司唯一的 PreviewKey。 只有知道 PreviewKey 的人才能下载你的预览包。

发布预览包的过程与发布任何其他包的过程相同，但需要将该包标识为预览除外，以便你选择的用户知道使用 PreviewKey。

对于公司合作伙伴提交的任何预览包，需要在注册表项中设置公司的 PreviewKey，进行以下设置：

- 注册表项：HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Device Metadata

- 值名称：DeviceMetadataPreviewKey

- 值类型：REG\_SZ

- 值：&lt;你的 PreviewKey&gt;

### <a name="to-create-a-previewkey"></a>创建 PreviewKey

1. 从合作伙伴中心使用 Microsoft 帐户登录仪表板。

2. 在窗口左侧，单击“设备元数据”  。

3. 在“设备元数据”  页的“管理预览密钥”  下，输入符合以下准则的 PreviewKey：

    - PreviewKey 必须包含 1 到 15 个字符。

    - 这些字符必须为字母数字。 换句话说，PreviewKey 只能包含大写字母、小写字母或数字。 PreviewKey 不能包含特殊字符。

    - PreviewKey 必须与任何其他现有 PreviewKey 均不同。

    - 每个公司仅允许使用一个 PreviewKey。

## <a name="related-topics"></a>相关主题


[创建设备元数据体验](create-a-device-metadata-experience.md)

[提交设备元数据包（仪表板帮助）](submit-a-device-metadata-package--dashboard-help-.md)

[设备元数据业务规则](device-metadata-business-rules.md)
