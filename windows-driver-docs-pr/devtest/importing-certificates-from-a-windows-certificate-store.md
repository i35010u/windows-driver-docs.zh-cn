---
title: 从 Windows 证书存储导入证书
description: 从 Windows 证书存储导入证书
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 131744a477729489dfa5c1538a8e16d511bc5955
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837321"
---
# <a name="importing-certificates-from-a-windows-certificate-store"></a>从 Windows 证书存储导入证书


你可以使用增强的存储证书管理工具将证书从计算机中的专用证书存储导入到符合 IEEE 1667 的 USB 存储设备。

若要从私有证书存储区导入证书，必须使用增强存储证书管理工具的 [**/add**](enhstor-add-switch.md)和 [**/Replace**](-replace-switch.md)开关的 **-store** 参数指定证书名称。 此工具将在所有专用证书存储中搜索指定的证书，如果找到，则 () 将其导入到指定的 USB 存储设备。

**注意**  该工具不会从 Windows 根证书存储中导入证书。

 

 

 





