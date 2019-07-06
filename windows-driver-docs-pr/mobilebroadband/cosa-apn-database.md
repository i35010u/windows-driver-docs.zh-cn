---
title: COSA/APN 数据库简介
description: COSA/APN 数据库简介
ms.assetid: 0E3DA610-090D-4D1E-B67E-A4747252E8BE
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: aa180797e13e7b649ba33d1a4363474bb2437322
ms.sourcegitcommit: 6f74454e7ed5e703e4e4b363b6816652950e6a51
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2019
ms.locfileid: "67608532"
---
# <a name="introduction-to-cosaapn-database"></a>COSA/APN 数据库简介

本部分包含有关 COSA 和 apndatabase.xml （APN 数据库） 的信息。 COSA 是使用 Windows 10，版本 1703年及更高版本，而对于 Windows 8，Windows 8.1 使用 APN 数据库和版本的 Windows 10，版本 1703年之前的 Windows 10 中的较新格式。

COSA 和 APN 数据库用于通过 Windows 网络组件，如 Windows 连接管理器中，为最终用户提供无缝连接体验，提供和尝试 APNs 基于用户的移动宽带设备的可用连接。 COSA 和 APN 数据库包含连接到移动宽带网络中，所需的信息允许 Windows 自动连接与最少的用户输入。 它们用于不同的移动网络运营，实现用户的连接之前获取的任何其他软件或元数据的运营商的网络维护访问字符串。 例如，用户可以获取连接而无需安装的移动宽带应用程序。

除了预配信息 COSA 和 APN 数据库还包含指向帐户体验网站的 URL。 自动连接到操作员的网络之后, 帐户体验在默认浏览器中的网站将打开，用户可以购买订阅或一次性访问。

下列主题进一步显示了有关 APNs、 COSA 及 APN 数据库。

- [APN 架构定义](apn-schema-definition.md)
- [APN 元素](apn-elements.md)
- [COSA 概述](cosa-overview.md)
- [APN 数据库概述](apn-database-overview.md)
- [COSA/APN 数据库提交](cosa-apn-database-submission.md)

