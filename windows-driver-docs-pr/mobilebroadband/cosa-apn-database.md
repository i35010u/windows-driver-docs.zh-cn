---
title: COSA/APN 数据库简介
description: COSA/APN 数据库简介
ms.assetid: 0E3DA610-090D-4D1E-B67E-A4747252E8BE
ms.date: 07/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: e0938cc8ccad492a78fc9d79caf1b7dd245b3f46
ms.sourcegitcommit: 7e4d9508198a30bdc1cb6eda83852dda4e42213e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89304296"
---
# <a name="introduction-to-cosaapn-database"></a>COSA/APN 数据库简介

本部分包含有关 COSA 和 apndatabase.xml (APN 数据库) 的信息。 COSA 是 Windows 10 版本1703及更高版本中使用的较新格式，而 APN 数据库用于 windows 10 的 windows 8、Windows 8.1 和 windows 10 版本1703之前的版本。

Windows 网络组件（如 Windows 连接管理器）使用 COSA 和 APN 数据库，通过基于用户的移动宽带设备提供和尝试可用的连接 APNs，为最终用户提供无缝连接体验。 COSA 和 APN 数据库包含连接到移动宽带网络所需的信息，从而允许 Windows 自动连接到最少的用户输入。 它们为不同的移动网络操作员维护访问字符串，使用户能够在获取任何其他软件或元数据之前连接到操作员的网络。 例如，用户可以在不安装移动宽带应用的情况下进行连接。

除了预配信息外，COSA 和 APN 数据库还包括帐户体验网站的 URL。 自动连接到操作员的网络后，将在默认浏览器中打开帐户体验网站，用户可以在其中购买订阅或一次性访问。

以下主题提供有关 APNs、COSA 和 APN 数据库的详细信息。

- [APN 架构定义](apn-schema-definition.md)
- [APN 元素](apn-elements.md)
- [COSA 概述](cosa-overview.md)
- [APN 数据库概述](apn-database-overview.md)
- [COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)

