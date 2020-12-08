---
title: 32 位和 64 位 WIA 互操作性
description: 32 位和 64 位 WIA 互操作性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25ba8b25b04a8b1650f7bd14cc87489cc32fe6f4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805589"
---
# <a name="32-bit-and-64-bit-wia-interoperability"></a>32 位和 64 位 WIA 互操作性


在运行扩展处理器的 Windows 64 位版本的系统上，所有 WIA 组件都是64位，因此 WIA 基础结构已更改，以允许这些64位驱动程序和现有的32应用程序之间的互操作性。

在64位版本的 Windows 操作系统上，64位 WIA 微型驱动程序在 WIA 服务的64位进程中加载。 但是，WIA 微型驱动程序 UI 扩展会加载到应用程序的进程空间中。 在基于 x64 的计算机上运行的 Microsoft Win32 应用程序的未修改32位进程将无法加载64位 UI 扩展。

为了降低32位的64位问题，Microsoft 提供了64位扩展主机， *wiawow64.exe*。 此主机确保32位应用程序与64位 WIA UI 扩展之间的透明互操作性。 *wiawow64.exe* 扩展主机将在适用于扩展处理器的 windows Server 2003 64 位版本中提供，适用于扩展处理器、windows Vista 和更高版本的操作系统版本的 windows XP 64 位版本。

WIA 服务将确定 UI 扩展的物理加载位置，具体取决于应用程序是64位还是32位：

-   *64 位应用程序*。 64位 WIA 微型驱动程序 UI 扩展直接加载到应用程序的进程空间中。 这类似于在32位版本的 Windows 操作系统上运行32位应用程序时所发生的情况。

-   *32 位应用程序*。 WIA 启动 UI 扩展将加载到的 *wiawow64.exe* 扩展主机。 每次从32位应用程序调用任何接口方法时，都将创建并启动 *wiawow64.exe* 的单独实例。 *wiawow64.exe* 主机在应用程序的上下文中运行，并通过现有的 COM 接口与应用程序进行通信。

    **注意**   尽管 *wiawow64.exe* 对 wia 应用程序编写器和 wia 驱动程序开发人员都是完全透明的，但驱动程序开发人员必须调试 *wiawow64.exe* 进程，而32不是调试64位 UI 扩展。

     

 

 




