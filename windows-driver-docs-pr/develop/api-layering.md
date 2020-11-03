---
ms.assetid: 9f14c40b-0d6a-45d0-9c8b-6c5603fee3c6
title: API 分层
description: 使用 Windows 驱动程序，可以创建一个在多种类型设备（从嵌入式系统到平板电脑和电脑）上运行的驱动程序。
ms.date: 04/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 6ff29eb62cc9e73cb1af0518bd9b219b07ca5163
ms.sourcegitcommit: f47c072e88dce59daba1231027b60eb56bd2cde9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/27/2020
ms.locfileid: "92689355"
---
# <a name="api-layering"></a>API 分层

## <a name="overview"></a>概述

API 分层要求，Windows 驱动程序包中的二进制文件只调用基于 UWP 的 Windows 10 版本中或特选 Win32 API 集中包含的 API 和 DDI。 API 分层是以前属于 DCHU 设计原则的“U”要求的扩展。

若要查看 API 支持哪个平台，请访问 API 的文档页，并审阅“要求”部分的“目标平台”条目。  Windows 驱动程序必须只使用将“目标平台”列为“`Universal`”（即在所有 Windows 产品/服务上都可用的功能的子集）的 API 或 DDI。

[Windows API 集](https://docs.microsoft.com/windows/win32/apiindex/windows-apisets)页面描述了一组最佳做法和工具，它们用于确定 API 是否适用于 Windows 10X 开发。

## <a name="validating-api-layering"></a>验证 API 分层  

[ApiValidator](/windows-hardware/test/hlk/testref/df4a9671-c2aa-4c81-b964-7247fb4799df) 是用于验证 Windows 驱动程序是否符合 API 分层要求的主要工具。  Windows 驱动程序工具包 (WDK) 随附 ApiValidator。  

若要详细了解如何使用 ApiValidator 来验证 Windows 驱动程序是否符合 API 分层要求，请参阅[验证 Windows 驱动程序](validating-windows-drivers.md)。
