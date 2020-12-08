---
title: 文件系统安全问题
description: 文件系统安全问题
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5992ea15050a56160398e72dd591fb88694759b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839553"
---
# <a name="file-system-security-issues"></a>文件系统安全问题


## <span id="ddk_file_system_security_issues_if"></span><span id="DDK_FILE_SYSTEM_SECURITY_ISSUES_IF"></span>


上一部分描述了一般术语中的安全注意事项。 除了对所有驱动程序感兴趣的一般安全问题之外，还有与文件系统相关的特定安全问题。 本部分试图为那些希望在其驱动程序中实现 Windows 样式安全性的文件系统提供指导。 本部分讨论了这些特定问题，以及如何在文件系统中解决这些问题。 本部分不是参考指南，也不提供所有可能的安全威胁的完整列表，以及如何缓解这些威胁。 不过，本部分的目的是识别众所周知的威胁和与安全性相关的关键问题，这些问题应由所有文件系统解决。 由于安全机制本身的范围很广，因此本文档并不介绍所有可能的安全问题或实现。

本节包括下列主题：

[语义模型检查](semantic-model-checks.md)

[安全检查](security-checks.md)

 

 




