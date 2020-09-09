---
title: INF SharedDriver 条目
description: INF SharedDriver 条目
ms.assetid: 36d094b4-481d-41bb-b034-345b0743456e
keywords:
- INF 文件 WDK 非 HID 键盘/鼠标
- SharedDriver entry WDK 非 HID 键盘/鼠标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51bb81000f66406dc602e79239d3a9022d4b4358
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592435"
---
# <a name="inf-shareddriver-entry"></a>INF SharedDriver 条目





**\[ControlFlags\]**

<em>SharedDriver</em> **=**<em>安装-名称</em>***、***<em>警告文本字符串</em>在键盘或鼠标类安装程序安装 PS/2 设备之前，它会检查设备[INF **ControlFlags**部分](../install/inf-controlflags-section.md)中的*SharedDriver*条目。 如果存在此类输入值，则类安装程序会通过显示警告文本字符串通知用户，并向用户提供取消更改 PS/2 端口驱动程序的选项。

### <a name="entries-and-values"></a>项和值

<a href="" id="shareddriver"></a>*SharedDriver*  
指定设备驱动程序由 PS/2 键盘和鼠标设备共享。

<a href="" id="install-section-name"></a>*安装-节名称*  
指定设备的 *DDInstall* 部分。

<a href="" id="warning-text-string"></a>*警告-文本字符串*  
指定一个字符串，在更改 PS/2 端口驱动程序之前，该类安装程序使用该字符串向用户发出警告。

 

