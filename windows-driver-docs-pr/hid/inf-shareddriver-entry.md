---
title: INF SharedDriver 条目
description: INF SharedDriver 条目
keywords:
- INF 文件 WDK 非 HID 键盘/鼠标
- SharedDriver entry WDK 非 HID 键盘/鼠标
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc23b30de9618542003a63f52b0ef6b83ac77d6f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819061"
---
# <a name="inf-shareddriver-entry"></a>INF SharedDriver 条目





**\[ControlFlags\]**

<em>SharedDriver</em> **=**<em>安装-节名称</em> **_，_* _ <em>警告文本字符串</em>在键盘或鼠标类安装程序安装 PS/2 设备之前，它会检查设备的 [INF **ControlFlags** 部分](../install/inf-controlflags-section.md)中是否存在 _SharedDriver * 项。 如果存在此类输入值，则类安装程序会通过显示警告文本字符串通知用户，并向用户提供取消更改 PS/2 端口驱动程序的选项。

### <a name="entries-and-values"></a>项和值

<a href="" id="shareddriver"></a>*SharedDriver*  
指定设备驱动程序由 PS/2 键盘和鼠标设备共享。

<a href="" id="install-section-name"></a>*安装-节名称*  
指定设备的 *DDInstall* 部分。

<a href="" id="warning-text-string"></a>*警告-文本字符串*  
指定一个字符串，在更改 PS/2 端口驱动程序之前，该类安装程序使用该字符串向用户发出警告。

 

