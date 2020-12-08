---
title: WIA 数据项
description: WIA 数据项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e59ab00250a4fb660d233d920a5b43d87971abd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824549"
---
# <a name="wia-data-item"></a>WIA 数据项





本主题适用于 Windows Vista 和更高版本。

可用于传输数据的任何项都被视为一个数据项。 这包括标记有 **WiaItemTypeProgrammableDataSource** 标志的项。 标记有 **WiaItemTypeTransfer** 标志的任何项都可以公开传输数据的功能。 具有此标志集的任何项都必须提供以下 WIA 属性：

[**WIA \_ IPA \_ 访问 \_ 权限**](./wia-ipa-access-rights.md)

[**WIA \_ IPA \_ 项 \_ 大小**](./wia-ipa-item-size.md)

[**WIA \_ IPA \_ 缓冲区 \_ 大小**](./wia-ipa-buffer-size.md)

[**WIA \_ IPA \_ 格式**](./wia-ipa-format.md)

[**WIA \_ IPA \_ 首选 \_ 格式**](./wia-ipa-preferred-format.md)

[**WIA \_ IPA \_ TYMED**](./wia-ipa-tymed.md)

[**WIA \_ IPA \_ 文件 \_ 扩展名**](./wia-ipa-filename-extension.md)

用 **WiaItemTypeTransfer** 标志标记的可编程数据源项必须提供这些 WIA 属性。 例如，平台扫描仪项必须具有这些属性才能正确配置数据传输。

WIA 数据项可能具有其他属性，具体取决于项的标志设置。 例如，使用 **WiaItemTypeImage** 标志标记的 WIA 项应具有图像特定的信息属性，例如 [**wia \_ IPA \_ DEPTH**](./wia-ipa-depth.md) 和 [**wia \_ IPA \_ \_ \_ 行号**](./wia-ipa-number-of-lines.md)。

 

