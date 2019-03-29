---
title: 32 位和 64 位 WIA 互操作性
description: 32 位和 64 位 WIA 互操作性
ms.assetid: f7f7a42a-590e-4f81-b325-ba9f9ffa9664
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59a4112f2dee1d23457d4d1fa3480a7eac758740
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566968"
---
# <a name="32-bit-and-64-bit-wia-interoperability"></a>32 位和 64 位 WIA 互操作性


在运行 Windows 64 位版本的扩展处理器的系统，WIA 的所有组件都是 64 位，因此 WIA 基础结构已更改为允许这些 64 位驱动程序和现有 32 位应用程序之间的互操作性。

在 64 位版本的 Windows 操作系统，64 位 WIA 微型驱动程序是在 WIA 服务的 64 位进程中加载。 但是，在应用程序的进程空间中加载 WIA 微型驱动程序 UI 扩展。 在基于 x64 的计算机运行的 Microsoft Win32 应用程序的未修改的 32 位进程将无法加载 64 位 UI 扩展。

若要缓解 32 位到 64 位问题，Microsoft 提供的 64 位扩展主机*wiawow64.exe*。 此主机可确保透明 32 位应用程序和 64 位 WIA UI 之间的互操作性扩展。 *Wiawow64.exe*扩展主机将在扩展处理器的 Windows Server 2003 64 位版本中，扩展处理器、 Windows Vista 和更高版本的操作系统版本的 Windows XP 64 位版本中提供。

WIA 服务将确定其中 UI 扩展以物理方式加载，具体取决于应用程序是 64 位或 32 位：

-   *64 位应用程序*。 64 位 WIA 微型驱动程序的 UI 扩展是直接加载到应用程序的进程空间。 这是类似于 32 位版本的 Windows 操作系统上运行的 32 位应用程序时，会发生什么情况。

-   *32 位应用程序*。 WIA 启动*wiawow64.exe* UI 扩展将被加载进扩展主机。 一个单独的实例*wiawow64.exe*被创建并启动到任何接口方法的调用来自 32 位应用程序每次。 *Wiawow64.exe*主机在与应用程序相同的上下文中运行，并与通过现有的 COM 接口的应用程序进行通信。

    **请注意**  即使*wiawow64.exe* WIA 应用程序编写器和 WIA 驱动程序开发人员，开发人员需要调试的驱动程序是完全透明的*wiawow64.exe*而不是要调试 64 位 UI 扩展的 32 位应用程序进程。

     

 

 




